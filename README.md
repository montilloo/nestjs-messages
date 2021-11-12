<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo_text.svg" width="320" alt="Nest Logo" /></a>
</p>

[circleci-image]: https://img.shields.io/circleci/build/github/nestjs/nest/master?token=abc123def456
[circleci-url]: https://circleci.com/gh/nestjs/nest

  <p align="center">A progressive <a href="http://nodejs.org" target="_blank">Node.js</a> framework for building efficient and scalable server-side applications.</p>
    <p align="center">
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/v/@nestjs/core.svg" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/l/@nestjs/core.svg" alt="Package License" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/dm/@nestjs/common.svg" alt="NPM Downloads" /></a>
<a href="https://circleci.com/gh/nestjs/nest" target="_blank"><img src="https://img.shields.io/circleci/build/github/nestjs/nest/master" alt="CircleCI" /></a>
<a href="https://coveralls.io/github/nestjs/nest?branch=master" target="_blank"><img src="https://coveralls.io/repos/github/nestjs/nest/badge.svg?branch=master#9" alt="Coverage" /></a>
<a href="https://discord.gg/G7Qnnhy" target="_blank"><img src="https://img.shields.io/badge/discord-online-brightgreen.svg" alt="Discord"/></a>
<a href="https://opencollective.com/nest#backer" target="_blank"><img src="https://opencollective.com/nest/backers/badge.svg" alt="Backers on Open Collective" /></a>
<a href="https://opencollective.com/nest#sponsor" target="_blank"><img src="https://opencollective.com/nest/sponsors/badge.svg" alt="Sponsors on Open Collective" /></a>
  <a href="https://paypal.me/kamilmysliwiec" target="_blank"><img src="https://img.shields.io/badge/Donate-PayPal-ff3f59.svg"/></a>
    <a href="https://opencollective.com/nest#sponsor"  target="_blank"><img src="https://img.shields.io/badge/Support%20us-Open%20Collective-41B883.svg" alt="Support us"></a>
  <a href="https://twitter.com/nestframework" target="_blank"><img src="https://img.shields.io/twitter/follow/nestframework.svg?style=social&label=Follow"></a>
</p>
  <!--[![Backers on Open Collective](https://opencollective.com/nest/backers/badge.svg)](https://opencollective.com/nest#backer)
  [![Sponsors on Open Collective](https://opencollective.com/nest/sponsors/badge.svg)](https://opencollective.com/nest#sponsor)-->

## Description

[Nest](https://github.com/nestjs/nest) framework TypeScript starter repository.

## Installation

```bash
$ npm install
```

## Running the app

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Test

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## Support

Nest is an MIT-licensed open source project. It can grow thanks to the sponsors and support by the amazing backers. If you'd like to join them, please [read more here](https://docs.nestjs.com/support).

## Stay in touch

- Author - [Kamil Myśliwiec](https://kamilmysliwiec.com)
- Website - [https://nestjs.com](https://nestjs.com/)
- Twitter - [@nestframework](https://twitter.com/nestframework)

## License

Nest is [MIT licensed](LICENSE).


## HTTP 请求是如何工作的

POST /messages/5?validate=true HTTP/1.1  --------Start line
HOST: localhost:3000                     --------Headers
Content-Type: application/json           --------Headers
{"content": "hi there"}                  --------Body

## Implementing a Service

我们的控制器将使用服务而不是存储库来访问数据。

服务正在创建自己的依赖项，messages 存储库是此服务的依赖项，换句话说，除非服务具有存储库，否则它不能正常工作。所以，我们在这两个类之间建立了依赖关系。并且该服务正在自行创建依赖关系，这是我们在Nest中不做的事情。我们没有让任何类在构造函数中创建自己的依赖项，相反，我们将在nest中使用一种非常特殊的系统，称为依赖项注入来设置。我们还没有这样做的原因是我想真正深入研究依赖项注入。帮助你真正深入理解这一切是怎么回事。`this.messagesRepo = new MessagesRepository();``这是一行非常临时的代码，稍后就会删除。我们将删除它，并依赖与依赖项注入来设置不同类之间的所有不同依赖关系。

## Manual Testing of the controller
我们已经完成了消息传递服务和存储库，所以现在我们需要创建一个实例并将其交给控制器，然后控制器将接收对我们的三个不同路由处理程序的传入请求，具体取决于在调用那个处理程序时，控制器将通过使用从服务中获得的数据来响应请求。

在controller中获得服务的实例 ，并使用它来响应请求。

## Reporting Errors with Exceptions

弄清楚这个未发现异常的东西是什么，这是一种在Nest内部被定义。如果在请求周期内抛出，Nest将自动捕获他们，并将其转换为非常漂亮的响应，以发送回给用户。

除了未找到异常之外，还在内部定义了几个其他异常。这些不同异常中的每一个都有点遵循HTTP标准设置的格式。

## Understanding Inversion of Control

理解依赖注入对您来说非常重要，但也有不利的一面。依赖注入有点复杂，除了复杂之外，理解它为什么存在可能是非常具有挑战性的。

我们将开始讨论，为什么存在依赖项注入。

![]("src/assets/images/1.png")

我们现在有了控制器服务和存储库，这些不同的类之间存在非常明显的依赖关系或层次结构，因此，服务依赖于存储库才能正常工作，如果该存储库不存在，我们的服务将无法正常工作，同样控制器依赖于服务，如果服务不存在，控制器将无法工作。在这三个不同的类之间，有非常明显的依赖关系。更重要的是现在我们的控制器和服务正在创建对其属于自己的。因此，当创建消息传递服务的实例时，该类都会自动独立创建自己的依赖关系。控制器也是如此，每当我们创建控制器的实例时，它都在创建自己的依赖项

控制反转，这是软件工程中的一个说法，如果您遵循这个原则，可能会更容易构建可重用代码或者编写可重用代码。这个原则是说，如果你想要有可重用的代码，你编写的类应该不自己创建他们自己依赖项的实例。

bad: MessagesService creates its own copy of MessagesRepository

```
  messagesRepo: MessagesRepository;

  constructor() {
    this.messagesRepo = new MessagesRepository();
  }
```
better: MessagesService receivers ite dependency

```
  messagesRepo: MessagesRepository;

  constructor(repo: MessagesRepository) {
    this.messagesRepo = repo;
  }
```

best: MessagesService receives its dependency, and it does't specifically require 'MessagesRepository'

```
  interface Repository {
    findOne(id: string);
    findAll();
    create(content: string);
  }

  export class MessagesService {
    messagesRepo: Repository;
    constructor(repo: Repository) {
      this.messagesRepo = repo;
    }
  }
```
在这里我们仍然有我们的消息服务，我们仍然期待被给予我们的依赖，但这一次我们不是特别想要获得消息存储库的副本，而是，相反，定义了一个简单的称为Repository的接口。我们说过，无论何时创建消息服务的副本或实例，都必须提供满足存储库接口的对象，所以这是最好的原因，因为我们并不依赖于消息库。只要您通过我们的代码，他就可以工作的非常好，任何满足此接口的对象都可以是消息库，它可以是具有完全不同实现的完全不同类型的存储库。

## Few More Notes on DI

容器将保持它已创建的所有实例的列表，因此，在依赖项注入领域理解这一点是非常重要的。每当容器创建依赖项时，每当创建消息服务实例或者存储库实例或其他任何东西，他将在内部存储该实例。如果再次请求相同的依赖项，可以随着时间的推移重用该实例。因此，如果您应用程序中有两个不同的类都请求消息服务，将只创建一个实例，并且该实例将在另外两个class上。