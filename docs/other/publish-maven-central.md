# Publish maven central

- Create a user in Sonartype.org (https://issues.sonatype.org/secure/Signup!default.jspa)

- Request ownership of group

  - Open a issue (https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134)

    ```
    Summary: Various java projects under "<GROUP:ID>" group id
    Description: Add links to project
    GroupId: <GROUP_ID>
    Project URL: <REPO_URL>
    SCM URL: <REPO_URL>
    ```

- Meet requirments (https://central.sonatype.org/publish/requirements/)

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <project xmlns="http://maven.apache.org/POM/4.0.0"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
  
      <groupId>io.github.devdevx</groupId>
      <artifactId>nothing</artifactId>
      <version>1.0.0-SNAPSHOT</version>
      <packaging>jar</packaging>
  
      <name>${project.groupId}:${project.artifactId}</name>
      <description>A demo for deployment to the Central Repository via OSSRH</description>
      <url>https://github.com/devdevx/nothing</url>
  
      <licenses>
          <license>
              <name>The Apache Software License, Version 2.0</name>
              <url>https://www.apache.org/licenses/LICENSE-2.0.txt</url>
          </license>
      </licenses>
  
      <developers>
          <developer>
              <id>author</id>
              <name>Adrian Palanques</name>
              <email>devdevx@mail.com</email>
          </developer>
      </developers>
  
      <scm>
          <connection>scm:git:git://github.com/devdevx/nothing.git</connection>
          <developerConnection>scm:git:ssh://github.com:devdevx/nothing.git</developerConnection>
          <url>https://github.com/devdevx/nothing/tree/master</url>
      </scm>
  
      <distributionManagement>
          <snapshotRepository>
              <id>ossrh</id>
              <url>https://oss.sonatype.org/content/repositories/snapshots</url>
          </snapshotRepository>
          <repository>
              <id>ossrh</id>
              <url>https://oss.sonatype.org/service/local/staging/deploy/maven2/</url>
          </repository>
      </distributionManagement>
  
      <properties>
          <maven.compiler.source>8</maven.compiler.source>
          <maven.compiler.target>8</maven.compiler.target>
  
          <maven-source-plugin.version>3.2.1</maven-source-plugin.version>
          <maven-javadoc-plugin.version>3.2.0</maven-javadoc-plugin.version>
          <maven-gpg-plugin.version>1.6</maven-gpg-plugin.version>
          <maven-enforcer-plugin.version>3.0.0-M3</maven-enforcer-plugin.version>
      </properties>
  
      <prerequisites>
          <maven>3.6.0</maven>
      </prerequisites>
  
      <build>
          <plugins>
              <plugin>
                  <groupId>org.apache.maven.plugins</groupId>
                  <artifactId>maven-source-plugin</artifactId>
                  <version>${maven-source-plugin.version}</version>
                  <executions>
                      <execution>
                          <id>attach-sources</id>
                          <goals>
                              <goal>jar-no-fork</goal>
                          </goals>
                      </execution>
                  </executions>
              </plugin>
              <plugin>
                  <groupId>org.apache.maven.plugins</groupId>
                  <artifactId>maven-javadoc-plugin</artifactId>
                  <version>${maven-javadoc-plugin.version}</version>
                  <executions>
                      <execution>
                          <id>attach-javadocs</id>
                          <goals>
                              <goal>jar</goal>
                          </goals>
                      </execution>
                  </executions>
              </plugin>
              <plugin>
                  <groupId>org.apache.maven.plugins</groupId>
                  <artifactId>maven-gpg-plugin</artifactId>
                  <version>${maven-gpg-plugin.version}</version>
                  <executions>
                      <execution>
                          <id>sign-artifacts</id>
                          <phase>verify</phase>
                          <goals>
                              <goal>sign</goal>
                          </goals>
                      </execution>
                  </executions>
              </plugin>
              <plugin>
                  <groupId>org.apache.maven.plugins</groupId>
                  <artifactId>maven-enforcer-plugin</artifactId>
                  <version>${maven-enforcer-plugin.version}</version>
                  <executions>
                      <execution>
                          <id>enforce-maven</id>
                          <goals>
                              <goal>enforce</goal>
                          </goals>
                          <configuration>
                              <rules>
                                  <requireMavenVersion>
                                      <version>3.6.0</version>
                                  </requireMavenVersion>
                              </rules>
                              <fail>true</fail>
                          </configuration>
                      </execution>
                  </executions>
              </plugin>
          </plugins>
      </build>
  
  </project>
  ```

- Generate GPD key (https://central.sonatype.org/publish/requirements/gpg/)

  - Windows

    - Download from https://www.gnupg.org/download/

    - Install only GnuPG

    - Commands

      ```
      gpg --list-keys
      gpg --list-secret-keys
      gpg --generate-key
      gpg --delete-secret-key <ID>
      gpg --delete-key <ID>
      gpg -a --export <ID> > key.pub
      gpg --import key.pub
      gpg --export-secret-keys <ID> > key.priv
      gpg --gen-revoke <ID> > key.revoc
      gpg --import key.revoc
      gpg --keyserver keys.openpgp.org --send-keys <ID>
      ```

- Package

  ```
  mvn package -Dgpg.passphrase=XXX
  ```

- Configure credentials

  ```
  <servers>
       <server>
          <id>ossrh</id>
          <username>user</username>
          <password>pass</password>
      </server>
  </servers>
  ```

- Deploy

  ```
  mvn deploy -Dgpg.passphrase=XXX
  ```

- Relese the artifacts

  - Login in https://s01.oss.sonatype.org/
  - Go to Staging repositories
  - Close repository
  - Release repository

- Validate in https://repo1.maven.org/maven2/