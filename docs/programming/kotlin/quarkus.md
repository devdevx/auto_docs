# Quarkus

## Main classes and annotations

### Web

- `@Path` 
- `@GET` 
- `@Produces` 
- `@PathParam`

### Reactive

- `@RestPath`

### DI

- `@Inject` (field with package access) 
- `@ApplicationScoped` 
- `@Superior` 
- `@Dependent` 
- `@Produces` 
- `@PostConstruct` 
- `@PreDestroy` 
- `@IfBuildProfile("prod")` 
- `@UnlessBuildProfile("test")` 
- `@IfBuildProperty(name = "some.tracer.enabled", stringValue = "true")` 
- `@UnlessBuildProperty(name = "some.tracer.enabled", stringValue = "false")` 

### Configuration

```java
@ConfigProperty(name = "greeting.suffix", defaultValue="!")
```

```java
String databaseName = ConfigProvider.getConfig().getValue("database.name", String.class);
Optional<String> maybeDatabaseName = ConfigProvider.getConfig().getOptionalValue("database.name", String.class);
```

````java
@StaticInitSafe
@ConfigMapping(prefix = "server")
interface Server {
    String host();
    int port();
}
````

### Testing

- `@QuarkusTest` 
- `@NativeImageTest`

### Reactive

- `Uni` 
- `Panache` 
- `PanacheEntity`

## Useful

`quarkus:dev` runs Quarkus in development mode. This enables hot deployment.

Dev UI in http://localhost:8080/q/dev/.

Use https://code.quarkus.io/ to generate projects.

Can define env vars in `.env` file in the root folder.

## Comands

### Maven

Build native executable

```
./mvnw package -Pnative -Dquarkus.native.container-build=true
./mvnw package -Pnative --define quarkus.native.container-build=true
```

Build native executable and a container

```
./mvnw quarkus:add-extension -Dextensions="container-image-docker"
./mvnw package -Pnative -Dquarkus.native.container-build=true -Dquarkus.container-image.build=true
./mvnw package -Pnative --define quarkus.native.container-build=true --define quarkus.container-image.build=true

./mvnw package -Pnative -Dquarkus.native.container-build=true -Dquarkus.container-image.build=true -Dquarkus.container-image.image=registry.com/name
./mvnw package -Pnative --define quarkus.native.container-build=true --define quarkus.container-image.build=true --define quarkus.container-image.image=registry.com/name
```

List and add extensions

````
./mvnw quarkus:list-extensions
./mvnw quarkus:add-extensions -Dextensions=ex1,ex2
````

### Gradle

**TODO:** Build native executable and container

List and add extensions

````
./gradlew listExtensions
./gradlew addExtension --extensions="ex1,ex2"
````

## Receipts

### Reactive REST with PostgreSQL

- **RESTEasy Reactive Jackson**

- **Hibernate Reactive with Panache**

- **Reactive PostgreSQL client**

## Learn

https://pattern-match.com/blog/quarkus-with-kotlin/

# TODO

https://quarkus.io/guides/getting-started-testing

# Reorder

https://www.composerize.com/

## Documentation

[Official documentation](https://quarkus.io/guides/)
