# NestJS

## Commands

Init

````
npm i -g @nestjs/cli
nest new project-name
````

Generate

````
nest g controller users
nest g service users
nest g module users
nest g resource users
````

Validations

````
npm i --save class-validator class-transformer
````

Config

````
npm install @nestjs/config
npm install --save joi
````

Database

````
npm install --save @nestjs/typeorm typeorm pg
````

Openapi

````
npm install --save @nestjs/swagger swagger-ui-express
````

> **`nest-cli.json.js`**
>
> ````
> {
>   "collection": "@nestjs/schematics",
>   "sourceRoot": "src",
>   "compilerOptions": {
>     "plugins": ["@nestjs/swagger"]
>   }
> }
> ````

Migrations

**TODO**: Validate

````
    migrations: ["dist/migrations/*{.ts,.js}"],
    migrationsTableName: "migrations_typeorm",
    migrationsRun: true
````

````
npx typeorm migration:generate -n RenameColInArticleTable -d src/migrations
````



## Main components

- Controllers
- Providers
- Modules
- Middleware
- Exception filters
- Pipes
- Guards
- Incerceptors
- Custom decorators

## Testing

````
npm i --save-dev @nestjs/testing
````

**TODO**: Add more info

## Techniques

- Persistence: Offers abstract layer and separated schema definition with TypeORM. Allows migration definition.
- Mapped Types: Allows to reuse DTOs for different operations.
- Built-in security with passport libs. CASL support is perfect for complex permission systems.
- Helmet helps secure common http mistakes.
- Has a plugin to generate OpenAPI documentation.
- Support GraphQL federation.

## Documentation

[Official documentation](https://docs.nestjs.com/)

[Complete guide](https://wanago.io/courses/api-with-nestjs/)

[Examples](https://github.com/nestjs/nest/tree/master/sample)

