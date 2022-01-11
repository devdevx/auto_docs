# Maven

## Dependencies

**Show dependency tree**
````bash
mvn dependency:tree
````

**Detect outdated dependencies**

[//]: #a (TODO: Investigate how to detect outdated dependencies in a friendly command line way)

**Update dependencies versions**
````bash
mvn versions:update-properties
mvn versions:update-parent
````

## Version
````bash
mvn help:evaluate -Dexpression=project.version -q -DforceStdout
````

## Publish single module project

````xml
    <distributionManagement>
        <snapshotRepository>
            <id>RESPOSITORY_ID</id>
            <url>REPOSITORY_URL</url>
        </snapshotRepository>
        <repository>
            <id>RESPOSITORY_ID</id>
            <url>REPOSITORY_URL</url>
        </repository>
    </distributionManagement>
````

````bash
mvn clean deploy
````

## Add repository

````xml
    <repositories>
        <repository>
            <id>RESPOSITORY_ID</id>
            <url>REPOSITORY_URL</url>
        </repository>
    </repositories>
````

## Release

````bash
mvn release:prepare

ask for current v
new v
and tag

mvn release:perform
````

TODO: Try and document

## Sonar

```xml
mvn verify sonar:sonar -Dsonar.host.url=XXX -Dsonar.login=TOKEN
```

## Jacoco

```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.7</version>
    <executions>
        <execution>
            <id>prepare-agent</id>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>prepare-package</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

```
mvn verify
```

## Dependency check

````xml
        <sonar.dependencyCheck.htmlReportPath>target/dependency-check-report.html</sonar.dependencyCheck.htmlReportPath>

            <plugin>
                <groupId>org.owasp</groupId>
                <artifactId>dependency-check-maven</artifactId>
                <version>6.1.5</version>
                <configuration>
                    <failBuildOnCVSS>6</failBuildOnCVSS>
                </configuration>
                <executions>
                    <execution>
                        <goals>
                            <goal>check</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
````

## Settings file

In `$HOME/.m2/settings.xml`

**Configure repository credentials**
````xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
  <servers>
    <server>
      <id>REPOSITORY_ID</id>
      <username>USERNAME</username>
      <password>PASSWORD</password>
    </server>
  </servers>
</settings>
````

