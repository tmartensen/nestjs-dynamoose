<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo_text.svg" width="320" alt="Nest Logo" /></a>
</p>

[travis-image]: https://api.travis-ci.org/nestjs/nest.svg?branch=master
[travis-url]: https://travis-ci.org/nestjs/nest
[linux-image]: https://img.shields.io/travis/nestjs/nest/master.svg?label=linux
[linux-url]: https://travis-ci.org/nestjs/nest

  <p align="center">A progressive <a href="http://nodejs.org" target="blank">Node.js</a> framework for building efficient and scalable server-side applications.</p>
    <p align="center">
<a href="https://www.npmjs.com/~nestjscore"><img src="https://img.shields.io/npm/v/@nestjs/core.svg" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/~nestjscore"><img src="https://img.shields.io/npm/l/@nestjs/core.svg" alt="Package License" /></a>
<a href="https://www.npmjs.com/~nestjscore"><img src="https://img.shields.io/npm/dm/@nestjs/core.svg" alt="NPM Downloads" /></a>
<a href="https://travis-ci.org/nestjs/nest"><img src="https://api.travis-ci.org/nestjs/nest.svg?branch=master" alt="Travis" /></a>
<a href="https://travis-ci.org/nestjs/nest"><img src="https://img.shields.io/travis/nestjs/nest/master.svg?label=linux" alt="Linux" /></a>
<a href="https://coveralls.io/github/nestjs/nest?branch=master"><img src="https://coveralls.io/repos/github/nestjs/nest/badge.svg?branch=master#5" alt="Coverage" /></a>
<a href="https://discord.gg/G7Qnnhy" target="_blank"><img src="https://img.shields.io/badge/discord-online-brightgreen.svg" alt="Discord"/></a>
<a href="https://opencollective.com/nest#backer"><img src="https://opencollective.com/nest/backers/badge.svg" alt="Backers on Open Collective" /></a>
<a href="https://opencollective.com/nest#sponsor"><img src="https://opencollective.com/nest/sponsors/badge.svg" alt="Sponsors on Open Collective" /></a>
  <a href="https://paypal.me/kamilmysliwiec"><img src="https://img.shields.io/badge/Donate-PayPal-dc3d53.svg"/></a>
  <a href="https://twitter.com/nestframework"><img src="https://img.shields.io/twitter/follow/nestframework.svg?style=social&label=Follow"></a>
</p>
  <!--[![Backers on Open Collective](https://opencollective.com/nest/backers/badge.svg)](https://opencollective.com/nest#backer)
  [![Sponsors on Open Collective](https://opencollective.com/nest/sponsors/badge.svg)](https://opencollective.com/nest#sponsor)-->

## Description

[Dynamoose](https://dynamoosejs.com/) module for [Nest](https://github.com/nestjs/nest).

## Installation

```bash
$ npm install nestjs-dynamoose dynamoose@beta
```

## Quick Start

A [Serverless NestJS Starter](https://github.com/hardyscc/aws-nestjs-starter) project has been created to demo the usage of this library, the following are some code gist.

1. App Module:

   ```ts
   import { DynamooseModule } from 'nestjs-dynamoose';
   ...

   @Module({
     imports: [
       ...
       DynamooseModule.forRoot({
         model: {
           create: false
         },
       }),
       UserModule,
     ],
   })
   export class AppModule {
   ```

2. User Schema:

   ```ts
   import { Schema } from 'dynamoose';
   import { SchemaAttributes } from 'nestjs-dynamoose';

   const schemaAttributes: SchemaAttributes = {
     id: String,
     name: String,
   };
   export const UserSchema = new Schema(schemaAttributes);
   ```

3. User Module:

   ```ts
   import { UserSchema } from './schema/user.schema';
   import { DynamooseModule } from 'nestjs-dynamoose';
   ...

   @Module({
     imports: [
       DynamooseModule.forFeature([
         { name: 'User', schema: UserSchema },
       ]),
     ],
     ...
   })
   export class UserModule {}
   ```

4. User Service

   ```ts
   import { InjectModel, Model } from 'nestjs-dynamoose';
   import * as uuid from 'uuid';
   ...

   @Injectable()
   export class UserService {
     constructor(@InjectModel('User') private userModel: Model<User>) {}

     create(input: CreateUserInput) {
       return this.userModel.create({
         ...input,
         id: uuid.v4(),
       });
     }
   }
   ```

## Support

Nest is an MIT-licensed open source project. It can grow thanks to the sponsors and support by the amazing backers. If you'd like to join them, please [read more here](https://docs.nestjs.com/support).

## License

Nest is [MIT licensed](LICENSE).
