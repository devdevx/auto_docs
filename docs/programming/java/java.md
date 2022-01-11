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

## Libraries

[Openhtmltopdf: HTML to PDF](https://github.com/danfickle/openhtmltopdf/wiki/Integration-Guide)

[Moneta: Manage money](https://mvnrepository.com/artifact/org.javamoney/moneta)

[Apache POI: Manage EXCEL files](https://mvnrepository.com/artifact/org.apache.poi/poi)

[Spring Boot: Framework](https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter)

[Liquibase: SQL Changelog](https://mvnrepository.com/artifact/org.liquibase/liquibase-core)

[MongoCK: MongoDB Changelog](https://www.mongock.io/)

[JSONassert](https://github.com/skyscreamer/JSONassert)

### Containerize

https://snyk.io/blog/best-practices-to-build-java-containers-with-docker/

## Patterns

https://java-design-patterns.com/patterns/

## Procedures

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

#### MAT (Eclipse Memory Analyzer Tool)

## Releases

https://openjdk.java.net/jeps/0

https://blogs.oracle.com/java/post/the-arrival-of-java-16

### Java 8

### Java 9

### Java 10

### Java 11

### Java 12

### Java 13

### Java 14

### Java 15

### Java 16

#### 1. New Language Features

##### **[JEP 394](https://openjdk.java.net/jeps/394)** **Pattern Matching for** **instanceof**

##### **[JEP 395](https://openjdk.java.net/jeps/395)** Records

#### 2. JVM Improvements

##### [JEP 376](https://openjdk.java.net/jeps/376) ZGC Concurrent Thread Processing

##### [JEP 387](https://openjdk.java.net/jeps/387) Elastic Metaspace

#### 3. New Tools and Libraries

##### [JEP 380](https://openjdk.java.net/jeps/380) Unix-Domain Socket Channels

##### [JEP 392](https://openjdk.java.net/jeps/392) Packaging Tool

#### 4. Futureproofing Your Work

##### **[JEP 390](https://openjdk.java.net/jeps/390)** Warning for Value-Based Classes

##### **[JEP 396](https://openjdk.java.net/jeps/396)** Strongly Encapsulate JDK Internals by default

#### 5. Incubator and Preview Features

##### **[JEP 338](https://openjdk.java.net/jeps/338) Vector API (Incubator)**

##### **[JEP 389](https://openjdk.java.net/jeps/389) Foreign Linker API (Incubator)**

##### **[JEP 393](https://openjdk.java.net/jeps/393) Foreign Memory Access API (3rd Incubator)**

##### **[JEP 397](https://openjdk.java.net/jeps/397) Sealed Classes (2nd Preview)**

#### 6. Improving Productivity for OpenJDK Developers

##### **[JEP 347](https://openjdk.java.net/jeps/347) Enable C++14 Language Features (in JDK source code)**

##### **[JEP 357](https://openjdk.java.net/jeps/357) Migrate from Mercurial to Git**

##### **[JEP 369](https://openjdk.java.net/jeps/369) Migrate to GitHub**

##### **[JEP 386](https://openjdk.java.net/jeps/386) Alpine Linux Port**

##### **[JEP 388](https://openjdk.java.net/jeps/388) Windows/AArch64 Port**

### Java 17 LTS

#### 1. Language features

##### [JEP 409](https://openjdk.java.net/jeps/409): Sealed classes

#### 2. Updates and Improvements on Core Libraries

##### [JEP 306](https://openjdk.java.net/jeps/306): Restore Always-Strict Floating-Point Semantics

##### [JEP 356](https://openjdk.java.net/jeps/356): Enhanced Pseudo-Random Number Generators

##### [JEP 382](https://openjdk.java.net/jeps/382): New macOS Rendering Pipeline

##### [JEP 415](https://openjdk.java.net/jeps/415): Context-Specific Deserialization Filters

#### 3. New Platform Support

##### [JEP 391](https://openjdk.java.net/jeps/391): macOS AArch 64 Port

#### 4. Previews and Incubators

##### [JEP 406](https://openjdk.java.net/jeps/406): Pattern Matching for switch (Preview)

##### [JEP 412](https://openjdk.java.net/jeps/412): Foreign Function and Memory API (Incubator)

##### [JEP 414](https://openjdk.java.net/jeps/414): Vector API (Second Incubator)

#### 5. Future Proofing Java Programs

##### [JEP 403](https://openjdk.java.net/jeps/403): Strongly Encapsulate JDK Internals

#### 6. Deprecations and Removals

##### [JEP 411](https://openjdk.java.net/jeps/411): Deprecate the Security Manager for Removal

##### [JEP 398](https://openjdk.java.net/jeps/398): Deprecate the Applet API for Removal

##### [JEP 407](https://openjdk.java.net/jeps/407): Remove RMI Activation

#### 7. For OpenJDK Contributors

##### [JEP 410](https://openjdk.java.net/jeps/410): Remove the Experimental AOT and JIT Compiler

