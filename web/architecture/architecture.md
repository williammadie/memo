# Web Architecture

## Table of Contents

- [SOLID Principles](#solid-principles)
- [Web Architecture](#web-architecture)
- [Pros and Cons of Clean Architecture](#pros-and-cons-of-clean-architecture)
- [Event-Driven Architecture](#event-driven-architecture)

## Architecture

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


## SOLID Principles

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

## Web Architecture

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

## Pros and Cons of Clean Architecture

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