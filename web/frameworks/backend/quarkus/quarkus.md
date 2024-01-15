# Quarkus

## Table of Contents

- [What is Quarkus](#what-is-quarkus)
- [Quarkus CLI](#quarkus-cli)
- [Historical Details](#historical-details)
    - [Java SE, Java EE and Jakarta EE](#java-se-java-ee-and-jakarta-ee)
    - [Spring and Quarkus](#spring-and-quarkus)
- [What is New](#what-is-new)
    - [Build Time Processing](#build-time-processing)
    - [Embedded Healthchecks](#embedded-healthchecks)
- [Hibernate ORM and JPA](#hibernate-orm-and-jpa)
- [Detached States](#detached-states)

## What is Quarkus

As modern frameworks do, Quarkus is centered around **performance**, **cloud-native support**, **micro-services** and **developer experience**.

As it is said on Quarkus official webpage: Quarkus applications are optimized for **low memory usage** and **fast startup times**.

## Arc Framework

Quarkus uses the `Arc` framework for implementing **CDI** (**Content Dependency Injection**).

## Quarkus CLI

Launch Quarkus Application with Hot reload and Dev UI
```bash
quarkus dev
```

Add an extension to `pom.xml`
```bash
quarkus extension add camel-quarkus-jackson
```

## Historical Details

### Java SE, Java EE and Jakarta EE

(history of all specifications)

### Spring and Quarkus

(history of both frameworks)

### What is New

### Build Time Processing

The central idea behind Quarkus is to do **at build-time what traditional frameworks do at runtime**:
- configuration parsing
- classpath scanning
- feature toggle based on classloading
- ...

In comparison to Spring, Quarkus does more checks at compiling/build time. For instance, it checks the validity of the `application.properties` file at compiling time.

### Embedded Healthchecks

In Quarkus, runtime capabilities such as **health checks** and **metrics** are exposed out of the box.

We only need to add the `smallrye-health` extension (see [Quarkus Smallrye Health](https://quarkus.io/guides/smallrye-health))

## Hibernate ORM and JPA

### Transactions

With JPA, it is possible to annotate methods with `@Transactional`. This implies that a transactional method will be completely executed or rollback. It is extremely important for keeping consistent states in our system.

```java
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

### Detached States

**Important**: When updating **a persisted object**, make sure to be inside the same transaction. If it leaves the method annotated with `@Transaction`, it will become **detached** which means that even if its attributes are changed it will not automatically update the DB.

In the below example, the issue is that we annotated our method with `@Transactional` however we receive an Entity that has been retrieved inside a previous transactions. This means that our updates will not affect our DB. In order to prevent this behavior, we simply have to annotate the method calling `depositMoneyToAccount()` (which should be a service method) so that it covers the whole process (retrieving + updating)

```java
@Transactional
public MoneyDepositDto depositMoneyToAccount(Account account, double amountToDeposit) {
    account.setBalance(account.getBalance() + amountToDeposit);
    return new MoneyDepositDto(
        account.getRib(),
        amountToDeposit,
        account.getBalance()
    );
}
```