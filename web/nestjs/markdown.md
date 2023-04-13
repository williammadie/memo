# NestJS

## Table of Contents

- [NestCLI](#nestcli)
- [NestJS Principles](#nestjs-principles)
  - [Controllers](#controllers)
  - [Providers](#providers)
  - [DTO](#dto)
  - [Interfaces](#interfaces)
- [NestJS Architecture](#nestjs-architecture)

## NestCLI

Installation
```bash
npm i -g @nestjs/cli
```

Create a new project (WITH TS STRICT MODE)
```bash
nest new --strict my-project-name
```

Create a new project
```bash
nest new my-project-name
```

Start server (inside project folder)
```bash
npm run start

# or

nest start
```

Start server in development mode (watch files changes)
```bash
npm run start:dev
```

## NestJS Principles

- NestJS is largely based on `decorators`. A lot of decorators are available inside the framework: `@Controller()`, `@Post()`, `@HttpCode()`... They add functionalities implicitely handled by the framework.

- As Angular, NestJS is strongly based on the `dependency injection` design pattern. Basically, this means that we can add class dependencies to a class when we instanciate it. The syntax looks like the following example:

An example of injecting a dependency at instanciation (CatsService)
```ts
// Constructor Based Injection
constructor(private catsService: CatsService) {}
```

- NestJS major concepts are **Controllers** and **Providers**. These two elements handles the majority of the tasks. Both ones **need to be defined** inside the `app.module.ts` file.

```ts
import { Module } from '@nestjs/common';
import { CatsController } from './cats/cats.controller';
import { CatsService } from './cats/cats.service';

@Module({
  controllers: [CatsController],
  providers: [CatsService],
})
export class AppModule {}
```

### Controllers

Controllers are responsible for handling **incoming requests** and returning **responses** to the client.

![controllers](/web/nestjs/resources/controllers.png)

Each controller has several routes with specialized actions:

![controller-routes](/web/nestjs/resources/controller-routes.png)

Definition of an endpoint handler for a GET request made at `/cats/list`
```js
import { Controller, Get } from '@nestjs/common';

@Controller('cats')
export class CatsController {
  @Get('list')
  myCustomMethod(): string {
    return 'This action returns all cats';
  }

  @Get('id/:id')
  myCustomMethod(@Param() params): string {
    console.log(params.id);
    return `This action returns details of the ${params.id} cat`;
  }

  // This endpoint uses the request content
  @Post('new')
  myOtherMethod(@Req() request: Request): string {
    return 'This action adds a new cat';
  }
}
```

#### Status Codes

Keep in mind that the response **status code** is always `200` by default, except for POST requests which are `201`.

This behavior can be changed with the decorator `@HttpCode(204)`.

#### Headers

It is possible to access the **response header** in order to build a custom one. You'll need to use the `@Header()` decorator.

#### Redirection

It is possible to redirect to another URL with the `@Redirect()` decorator.

### Providers

Providers are a fundamental concept in NestJS. They refer to **services, repositories, factories, helpers and so on**. Providers are **injected as a dependency**.

### DTO

**DTO** stands for **Data Transfer Object**. It is an object that defines how an object will be sent over the network. It is typically a class looking like the following example:

```ts
export class CreateCatDto {
  name: string;
  age: number;
  breed: string;
}
```

Then it is used inside Controllers like in the following example:

```ts
@Post()
async create(@Body() createCatDto: CreateCatDto) {
  return 'This action adds a new cat';
}
```

### Interfaces



## NestJS Architecture

NestJS is organized by concepts. For instance, every information linked to the concept of `Cats` will be organized under the `src/cats/` folder.

Inside the `cats/` folder, we'll find:
- **Controllers**
- **Providers**
- **DTO Schemas** (**Data Transfer Object**) 
- **Interfaces**

```bash
src/
├── app.controller.spec.ts
├── app.controller.ts
├── app.module.ts
├── app.service.ts
├── cats
│   ├── cats.controller.ts
│   ├── cats.service.ts
│   ├── dto
│   │   └── create-cat.dto.ts
│   └── interfaces
│       └── cat.interface.ts
└── main.ts
```