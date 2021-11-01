The Malagu framework can be easily integrated with third-party database operation frameworks, such as Sequelize and TypeORM. Malagu's component mechanism increases the extensibility of third-party libraries and supports attribute configuration for out-of-the-box use.

Currently, Malagu offers integration with TypeORM libraries. You can configure the database connection information through the framework configuration file. In addition, Malagu is serverless-first, so it features best practice adaption to serverless scenarios during integration with TypeORM. In addition, it draws on the Spring transaction management mechanism to provide non-intrusive transaction management capabilities and support transaction propagation behaviors.


## Directions
1. The framework provides a built-in template `database-app`. You can run the following command to quickly initialize a template application related to database operations:
```sh
malagu init demo database-app
```
2. After the initialization is completed, you only need to change the database connection to the connection in the current actual environment. You can also install the `@malagu/typeorm` component directly in the project by running the following command:
```sh
yarn add @malagu/typeorm 
# Or, run `npm i @malagu/typeorm`
```

## Configuring Data Source Connection

The data source connection configuration in Malagu is similar to that in TypeORM, with slightly different configuration form and location. In order to keep the configuration method for third-party libraries consistent with that for framework components, the framework adapts the original configuration method of TypeORM to that for framework components during integration with TypeORM. For more information on TypeORM data source connection configuration, please see [Connection Options](https://typeorm.io/#/connection-options).


<dx-tabs>
::: Single data source
If the data source connection name is not set, it will be `default` by default.
```
# malagu.yml
backend: 
  malagu:
    typeorm:
      ormConfig:
        - type: mysql
          host: localhost
          port: 3306
          synchronize: true
          username: root
          password: root
          database: test
```
:::
::: Multiple data sources
In order to distinguish between different data source connections, you need to set a name for each connection. There can be one and only one connection with no name set, and its name will be `default` by default. When OrmContext APIs are used, the data source connection names will be used.
```
# malagu.yml
backend: 
  malagu:
    typeorm:
      ormConfig:
        - type: mysql
          host: localhost
          port: 3306
          synchronize: true
          username: root
          password: root
          database: test
        - type: mysql
        	name: 'datasource2'
          host: xxxx
          port: 3306
          synchronize: true
          username: root
          password: root
          database: test
```
:::
</dx-tabs>



## Database Operation

The following sample uses the RESTful style to implement APIs.
>?You can also use the RPC style for implementation, and these two styles are similar.

```
import { Controller, Get, Param, Delete, Put, Post, Body } from '@malagu/mvc/lib/node';
import { Transactional, OrmContext } from '@malagu/typeorm/lib/node';
import { User } from './entity';

@Controller('users')
export class UserController {
    @Get()
    @Transactional({ readOnly: true })
    list(): Promise<User[]> {
        const repo = OrmContext.getRepository(User);
        return repo.find();
    }
    @Get(':id')
    @Transactional({ readOnly: true })
    get(@Param('id') id: number): Promise<User | undefined> {
        const repo = OrmContext.getRepository(User);
        return repo.findOne(id);
    }
    @Delete(':id')
    @Transactional()
    async reomve(@Param('id') id: number): Promise<void> {
        const repo = OrmContext.getRepository(User);
        await repo.delete(id);
    }
    @Put()
    @Transactional()
    async modify(@Body() user: User): Promise<void> {
        const repo = OrmContext.getRepository(User);
        await repo.update(user.id, user);
    }
    @Post()
    @Transactional()
    create(@Body() user: User): Promise<User> {
        const repo = OrmContext.getRepository(User);
        return repo.save(user);
    }
}
```

## Database Context

In Malagu, TypeORM's transactions are managed by the framework, which provides the `@Transactional` decorator for how the framework initiates, propagates, commits, and rolls back transactions before and after execution methods. Plus, the framework puts the managed EntityManager objects in the database context for easy use by the business code. In addition, you can also manually manage database transactions and create EntityManager objects.

The database context is implemented based on the request context, so it is also at the request level. It mainly provides methods to get EntityManager and Repository objects:
```
export namespace OrmContext {
    export function getEntityManager(name = DEFAULT_CONNECTION_NAME): EntityManager {
        ...
    }
    export function getRepository<Entity>(target: ObjectType<Entity>|EntitySchema<Entity>|string, name?: string): Repository<Entity>  {
		    ...
    }
    export function getTreeRepository<Entity>(target: ObjectType<Entity>|EntitySchema<Entity>|string, name?: string): TreeRepository<Entity>  {
			  ...
    }
    export function getMongoRepository<Entity>(target: ObjectType<Entity>|EntitySchema<Entity>|string, name?: string): MongoRepository<Entity>  {
        ...
    }
    export function getCustomRepository<T>(customRepository: ObjectType<T>, name?: string): T {
        ...
    }
    export function pushEntityManager(name: string, entityManager: EntityManager): void {
        ...
    }
    export function popEntityManager(name: string): EntityManager | undefined {
        ...
    }
}
```

## Transaction Management

Malagu provides the `@Transactional` decorator to define the behaviors of transactions in a declarative manner. It decides the opening, propagation, commit, and rollback behaviors of transactions according to the decorator's declaration.

### @Transactional

The `@Transactional` decorator can be added to classes and methods. If it is added to a class and a method at the same time, the final configuration will be to use the configuration of the method to merge the class, which has a higher priority than the class. The decorator configuration options are as follows:
```
export interface TransactionalOption {
    name?: string;              // In case of multiple data source connections, specify the data source connection name, which is `default` by default
    isolation?: IsolationLevel; // Database isolation level
    propagation?: Propagation;  // Transaction propagation behavior. Valid values: Required, RequiresNew. Default value: Required
    readOnly?: boolean;         // Read-only mode, i.e., not to start transaction. Transaction is started by default
}
```
Below is a sample:
```
@Put()
@Transactional()
async modify(@Body() user: User): Promise<void> {
  const repo = OrmContext.getRepository(User);
	await repo.update(user.id, user);
}
```

### @Transactional and OrmContext

According to the configuration of the decorator, Malagu starts (or does not start) a transaction before invoking a method and hosts the EntityManager in the OrmContext context. OrmContext is fetched to the framework to assist with the EntityManager that has started a transaction, where the repository is created by the managed EntityManager. In order to get the EntityManager correctly, please make sure that the configured name of the decorator is the same as that of the EntityManager to be obtained through OrmContext. If you don't specify a name, the default value will be `default`.

After the method is executed, the framework automatically determines whether to commit or roll back the transaction according to the method execution. If the method execution is exceptional, the transaction will be rolled back; otherwise, it will be committed.

If the method has nested invocations to another method with the `@Transactional` decorator, the configuration of transaction propagation behavior determines whether to reuse the transaction of the upper-layer method or start a new one.


### Database query

In most cases, database queries do not require starting transactions, but we recommend you add the `@Transactional` decorator to the method and configure `readonly` to `true`, so that the framework can create an EntityManager that does not start transactions and maintain a uniform code style. Below is a sample:
```
@Get()
@Transactional({ readOnly: true })
list(): Promise<User[]> {
  const repo = OrmContext.getRepository(User);
	return repo.find();
}
```

### Transaction propagation behavior

Transaction propagation behaviors determine how transactions are propagated between different methods that require transactions. Currently, two transaction propagation behaviors are supported:
```
export enum Propagation {
    Required, RequiresNew
}
```
- **Required**: a transaction needs to be started. If the upper-layer method has already started one, it will be reused; otherwise, a new one will be started.
- **RequiresNew**: no matter whether the upper-layer method has started a transaction, a new transaction will be started.

>!When a transaction is propagated in different methods, please make sure that the methods are invoked synchronously. Below is a sample: 
```
...
@Transactional()
async foo(): Promise<void> {
  ...
  await bar();  // `await` must be added
}
....

...
@Transactional()
async bar(): Promise<void> {
  ...
}
```


## Binding Entity Class

The framework provides the `autoBindEntities` method for binding entity classes, which is generally invoked in the module entry file and contains the following two parameters:
- **entities**: entity class you defined.
- **name**: data source connection you want to bind to the entity class, which is `default` by default.

```
export function autoBindEntities(entities: any, name = DEFAULT_CONNECTION_NAME) {
}
```

Below is a sample:
```
import { autoBindEntities } from '@malagu/typeorm';
import * as entities from './entity';
import { autoBind } from '@malagu/core';

autoBindEntities(entities);
export default autoBind();
```

## Tools


| Tool | Description | 
|---------|---------|
| DEFAULT_CONNECTION_NAME	 | The default database connection name is `default`. | 
| autoBindEntities | Binds entity class. | 


