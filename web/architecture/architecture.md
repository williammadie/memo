# Web Architecture

## Table of Contents

- [Fundamentals](#fundamentals)
    - [SOLID Principles](#solid-principles)
    - [Web Architecture](#web-architecture)
- [Clean Architecture](#clean-architecture)
- [Event-Driven Architecture](#event-driven-architecture)
- [ServiceLayer Architecture](#servicelayer-architecture)
    - [DAO and Repository](#dao-and-repository)
    - [DTO and Entity](#dto-and-entity)

## Fundamentals 

### Architecture

Concretly, architecture refers to the following principles:

- `Components`

- `MVC`

- `Monolithic`

- `Microservices`

- `Clean Architecture`

- `SOLID`

- `Environment Management`

- `Application Hosting Management`

- `Paradigm`


### SOLID Principles

- `S`: **Single Responsability Principle**: A module, a class, a function or a method should have only one unique responsability.

*example*: If we have a class `Drawer`, it should not have both methods `draw()` and `erase()`. These two functions should be separated in two different classes. 

- `O`: **Open/Closed Principle**: A class should be opened in extension and closed in modification. (Use inheritance mechanisms) 

*example*: 

- `L`: **Liskov Substitution Principle**: A software should not break if we use a parent implementation instead of a child class.

*example*: If we have a parent interface `Animal` and a child class `Cat`. We should be able to instantiate x of type Cat and y of type Animal without destroying.

- `I`: **Interface Segregation Principle**: We should prefer the use of several small interfaces than one heavy interface.

*example*: If we have a class `Cat`, it should inherits from several interfaces (`Animal`, `Mammal`, `Feline`...)

- `D`: **Dependency Inversion Principle**: Dependencies should rely on abstraction and not implementation

*example*: We have two classes `ScyllaDB` and `PostgresDB` and a class `DBReport`. We should not rely on a specific type of database but instead use an interface `DBInterface` that we specify in the `DBReport` constructor.

### Web Architecture

*monolith architecture*: single codebase.

*serverless*: server that is sleeping when not required. It wakes up only when a user needs it. It is mainly used for functions that are not called very often.

*microservice/web-services*: application layer is divided into small services that communicate together through an API Gateway. Each unit is very easy to scale has it is independent.

**API Gateway**: Entry gate that authorizes external/end-user requests. Then, the different APIs are not exposed. They are on an internal network.

|               **Monolith Architecture**              |                           **Serverless**                          | **3-Tier**                                                                                                                                  |                                                                      **Microservices**                                                                      |
|:----------------------------------------------------:|:-----------------------------------------------------------------:|---------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------:|
|                 Difficult to maintain                |                             Very cheap                            | Tier 1 : UI                                                                                                                                 |                                                  Application layer is divided into small independent units.                                                 |
|                  Difficult to scale                  | Auto-scaling (Resources are auto-managed by the hosting provider) | Tier 2 : Application Layer                                                                                                                  |                             Each service has its own database. It is more secure as there is no more a single point of failure.                             |
|        Enforce the usage of a single language        |        Very slow on first call because it needs to wake up        | Tier 3 : Database Layer                                                                                                                     |                                                                        Money economy                                                                        |
| Fast to setup. Used a lot for PoC (Proof of Concept) |                      Add complexity in setup                      | Difficult to maintain/scale because the application layer is going to scale up. However, this part is a monolith. (Solution: microservices) |                                                   Each unit is a new codebase. More simple for developers.                                                  |
|                                                      |       Very difficult to migrate to another hosting provider       |                                                                                                                                             | Add a lot of complexity on the network. Heavily disadvised if we don't have several teams specialized in network connectivity. More complicated for devOps. |
|                                                      |                                                                   |                                                                                                                                             | Deployment is more complicated as each unit must be deployed with its own database and API gateways.                                                        |
|                                                      |                                                                   |                                                                                                                                             | Versioning is more complicated as each update on unit could affect others units.                                                                            |

## Clean Architecture

**Clean Architecture** is a type of system architecture organized by layers and proposed by **Robert C. Martin** (aka Uncle Bob).

1. External elements for my application: External interfaces / API (Stripes, ) / DB / Mailer
2. Communicate with my application: Gateways / Controllers / Presenters
3. Use Cases: Application Business Rules ([FR] Code Métier)
4. Entities/Domain: All our classes (Manga, User, UserManga)

Application Business Rules: Code related to the business core of a company. The most important code in our software. 

![schema-clean-architecture](/web/architecture/resources/schema-clean-archi.png)

**Important Note**: Internal layers (let's say we take entities) should not depend on external layers (such as use cases, controllers...)

YT: primogem

### Pros and Cons of Clean Architecture

Pros:
- SOLID Principles compliant
- Less coupling between classes
- Very easy to maintain and to add new features

Cons:
- Need a Long time to master
- Need more code

## Event-driven Architecture

For micro-services, we talk about **event-driven architecture**. 

For instance, if one unit/micro-service is updated (a user changes his email address), other micro-services might need to update too if they need this information. In that case, we use an **Event Broker**: 

![schema-ms-event-broker](/web/architecture/resources/ms-event-broker.png)

Keep in mind that in reality, systems are often mixed between micro-services (MS) and Monolith architectures.


Why does the 3-tier architecture respects SOLID principles?

## ServiceLayer Architecture

**ServiceLayer Architecture** is the name of the famous legacy architecture of applications built with SpringBoot. For people who likes diagrams, it refers to this organization between layers:

![service-layer-architecture](/web/architecture/resources/service-layer-architecture.png)

In a ServiceLayer Architecture, there are **3 layers**:
1. Domain Model/Entity (Business Layer)
2. Series of REST Endpoints (Presentation Layer)
3. A means for storing domain objects (Persistence Layer)

### DAO and Repository

Both are design patterns that aims at encapsulating the logic of interactions wih DB.

`DAO` stands for `Data Access Object`. It is simply a class that holds methods for accessing the DB. You typically write them as your project progresses.

`Repository` is a sort of enriched DAO with predefined methods for doing basic actions like retrieving an object or a list of objects based on filters...

### DTO and Entity

In this kind of architecture, layers communicates with `DTO` (`Data Tranfer Object`) also called `VO` (`Value Object`). The only difference between a DTO and a VO is that VO is supposed to be **immutable**. The are commonly used interchangeably.

In the same manner, there is also `Domain Model` that refers to the same concept as `Entity` and that is used interchangeably.

In a nutshell:

- DTO = VO
- Entity = Domain Model

I recently found the following diagram on the Web and tried to apply it in one of my application only to realize it was not a **viable option**. Why? Let's see:

![dto-or-entity](/web/architecture/resources/dto-or-entity.png)

The top solution recommends that our DAO returns DTOs. Like that, each layer uses DTOs to communicate. However, this work only for extremely simple applications. 

Let's say I'm creating a financial application that needs to handle money transfers. My DAO contains methods to add and remove money to a bank account and a method to retrieve a specific account.

DAOs should always be as simple as possible and business logic should always resides inside Services. So, I decide to put all money transfer logic (validation, account retrieving, account modifications) inside a Service. And here comes our problem. If DAOs only return DTOs, I'm forced to have an interface like the following: 

```java
public interface AccountDao {

    void addMoneyToAccount(UUID accountId);

    void removeMoneyFromAccount(UUID accountId);

    AccountDto findAccountById(UUID accountId);
}
```

And then we have our money transfer method inside our service. This method does a bit of validation and then executes the transfer:

```java
public class AccountServiceImpl implements AccountService {

    @Inject
    AccountDao accountDao;

    @Transactional
    void transferMoney(UUID sourceAccountId, UUID targetAccountId, double amount) {
        AccountDto sourceAccountDto = accountDao.findAccountById(sourceAccountId);
        AccountDto targetAccountDto = accountDao.findAccountById(targetAccountId);

        AccountValidation.validate(sourceAccountDto, targetAccountDto)

        accountDao.removeMoneyFromAccount(sourceAccountId);
        accountDao.addMoneyToAccount(targetAccountId);
    }
}
```

*Note that I voluntarily removed Optionals to increase readibility. But always use Optional!!!*

Here, we have **a grand total of 4 database requests**:
- 2 for finding source and target accounts inside our Service
- 2 for finding source and target accounts inside our Dao

This is **complete garbage in terms of performance** as each I/O operation like a DB request is extremely expensive.

So how do we fix it? We simply break the rule of the DTO and authorize our DAO to return Entities:

```java
public interface AccountDao {

    void addMoneyToAccount(Account account);

    void removeMoneyFromAccount(Account account);

    Account findAccountById(UUID accountId);
}

public class AccountServiceImpl implements AccountService {

    @Inject
    AccountDao accountDao;

    @Transactional
    void transferMoney(UUID sourceAccountId, UUID targetAccountId, double amount) {
        Account sourceAccount = accountDao.findAccountById(sourceAccountId);
        Account targetAccount = accountDao.findAccountById(targetAccountId);

        AccountValidation.validateTransfer(sourceAccount, targetAccount, amount);

        accountDao.removeMoneyFromAccount(sourceAccount);
        accountDao.addMoneyToAccount(targetAccount);
    }
}
```

Here we are! We divided our number of I/O operations by 2. **We now have 2 requests** for finding source and target accounts.