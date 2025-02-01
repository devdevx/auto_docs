# Java

## Procedures

### Configure multiple versions

1. Install all the versions that you want
2. Set the `JAVA_HOME` env var to the most recent and stable version
3. Remove from the `Path` env var all the paths related to java
4. Add the `%JAVA_HOME%\bin` to `Path` env var
5. Create a script for each configurable version
```` title="java17.bat"
@echo off
set JAVA_HOME=C:\Program Files\Java\jdk-17
set Path=%JAVA_HOME%\bin;%Path%
echo Java 17 activated.
````
6. Add the script folder to `Path` env var 
7. Execute the file name of the script each time you want to change the version

### Detect memory leak

#### VisualVM

##### Remote Java process

Start program with:

````bash
java
-Dcom.sun.management.jmxremote
-Dcom.sun.management.jmxremote.port=9010
-Dcom.sun.management.jmxremote.rmi.port=9010
-Dcom.sun.management.jmxremote.local.only=false
-Dcom.sun.management.jmxremote.authenticate=false
-Dcom.sun.management.jmxremote.ssl=false
-jar app.jar
````

## Libraries

[Openhtmltopdf: HTML to PDF](https://mvnrepository.com/artifact/io.github.openhtmltopdf/openhtmltopdf-core) ([Repo](https://github.com/openhtmltopdf/openhtmltopdf))

[Moneta: Manage money](https://mvnrepository.com/artifact/org.javamoney/moneta) ([Repo](https://github.com/JavaMoney/jsr354-ri))

[Apache POI: Manage EXCEL files](https://mvnrepository.com/artifact/org.apache.poi/poi)

[Spring Boot: Framework](https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter) ([Repo](https://github.com/spring-projects/spring-boot))

[Liquibase: SQL Changelog](https://mvnrepository.com/artifact/org.liquibase/liquibase-core) ([Repo](https://github.com/liquibase/liquibase))

[MongoCK: MongoDB Changelog](hhttps://mvnrepository.com/artifact/io.mongock/mongock-api) ([Repo](https://github.com/mongock/mongock))

[JSONassert](https://mvnrepository.com/artifact/org.skyscreamer/jsonassert) ([Repo](https://github.com/skyscreamer/JSONassert))

## Containerize

[Good practices](https://snyk.io/blog/best-practices-to-build-java-containers-with-docker/)

## Patterns

[List](https://java-design-patterns.com/patterns/)

## Releases

### Java 25 (LTS)

### Java 24

### Java 23

#### Pattern Matching for Primitive Types

```java
int x = 55;
switch (x) {
    case 200 -> System.out.println("OK");
    case 404 -> System.out.println("Resource Not Found");
    case 500 -> System.out.println("Internal Server Error");
    case int k -> System.out.println("Unknown status: " + k);
}
```

### Java 22

#### Structured Concurrency

```java
import java.util.concurrent.*;

public void downloadFiles(List<String> fileUrls) throws InterruptedException, ExecutionException {
    try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
        List<Future<?>> futures = new ArrayList<>();
        for (String url : fileUrls) {
            futures.add(executor.submit(() -> downloadFile(url)));
        }
        for (Future<?> future : futures) {
            future.get();
        }
    }
}
```

#### Statements Before Super

```java
public class Rectangle extends Shape {
    private int width;
    private int height;

    public Rectangle(int width, int height, String color) {
        this.width = width;
        this.height = height;
        super(color);
  }
}
```

#### Unnamed Variables

```java
String result = switch (expression) {
    case Integer _ -> "Integer";
    case String _ -> "String";
    default -> "Unknown";
};
```

#### String Literal (Preview)

```java
String name = "Bob";
String welcomeText = STR."Welcome \{name}";
```

```java
double price1 = 10.5;
double price2 = 20.75;
String result = FMT."$%.2f\{price1} + $%.2f\{price2} = $%.2f\{price1 + price2}";
```

### Java 21 (LTS)

#### Record Patterns

```java
record Point(int x, int y) {}
 
public static int recordPattern(Object obj) {
    if(obj instanceof Point(int x, int y)) {
        return x+y;
    }
    return 0;
}
```

#### Pattern Matching for switch

```java
double result = 0;
switch (account) {
    case null -> throw new RuntimeException("No account");
    case SavingsAccount sa -> result = sa.getSavings();
    case TermAccount ta -> result = ta.getTermAccount();
    case CurrentAccount ca -> result = ca.getCurrentAccount();
    default -> result = account.getBalance();
};
```

```java
String output = null;
switch(input) {
    case null -> output = "NULL";
    case String s when "Yes".equalsIgnoreCase(s) -> output = "Yes";
    case String s when "No".equalsIgnoreCase(s) -> output = "No";
    case String s -> output = "Try Again";
}
return output;
```

#### Virtual Threads

Virtual threads are lightweight threads with the purpose of reducing the effort of developing high-concurrent applications. Many virtual threads can share OS threads to run their code.

```java
try(var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    IntStream.rangeClosed(1, 10_000).forEach(i -> {
        executor.submit(() -> {
            System.out.println(i);
            try {
                Thread.sleep(Duration.ofSeconds(1));
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
    });
}
```

#### Sequenced Collections

```java
interface SequencedCollection<E> extends Collection<E> {
    SequencedCollection<E> reversed();
    void addFirst(E);
    void addLast(E);
    E getFirst();
    E getLast();
    E removeFirst();
    E removeLast();
}
```

```java
interface SequencedSet<E> extends Set<E>, SequencedCollection<E> {
    SequencedSet<E> reversed();
}
```

```java
interface SequencedMap<K, V> extends Map<K, V> {
    SequencedMap<K, V> reversed();
    SequencedSet<K> sequencedKeySet();
    SequencedCollection<V> sequencedValues();
    SequencedSet<Entry<K, V>> sequencedEntrySet();
    V putFirst(K, V);
    V putLast(K, V);
    Entry<K, V> firstEntry();
    Entry<K, V> lastEntry();
    Entry<K, V> pollFirstEntry();
    Entry<K, V> pollLastEntry();
}
```

### Java 17 (LTS)

#### Pattern matching

```java
if (obj instanceof String s) {
    System.out.println(s.length());
}
```

#### Switch expression

```java
int day = 3;
String result = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    default -> "Invalid day";
};
```

### Java 11 (LTS)

#### `var`

```java
var value = "the value";
```

#### `String` methods

```java
String str = " Java 11 ";
str.isBlank();
str.strip();
str.lines();
```

#### `Files` methods

```java
Files.writeString(Paths.get("example.txt"), "Hello, Java 11");
```

#### HTTP Client API

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://example.com"))
    .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
```