# GitlabCI

## Explore

https://www.notion.so/100DaysOfKubernetes-0c1e0de84d654e59bdf89242195abb22

## File structure

File should be named `.gitlab-ci.yml` and be in the root folder.

````yaml
image: <BASE_IMAGE>

services:
  - <BASE_SERVICE_1>
  
stages:
  - <STAGE_1>

before_script:
  - <SCRIPT_COMMAND>
  
after_script:
  - <SCRIPT_COMMAND>
  
include:
  - <TEMPLATE_TO_INCLUDE>

variables:
  <VARIABLE_1>: <VALUE_1>
  
cache:
  paths:
    - <PATH_1>
  key: <CACHE_KEY>

<JOB_NAME_1>:
  image: <JOB_IMAGE>
  stage: <JOB_STAGE>
  services:
    - <SERVICE_1>
  script:
    - <SCRIPT_COMMAND>
  artifacts:
    paths:
      - <ARTIFACT_PATH_1>
    expire_in: <TIME_EXPRESION>
````

## Common schemes

### Merge request validation

Validate the source branch of a merge request and block merge if don't meets the criteria.

```yaml
variables:
  MAVEN_OPTS: "-Dhttps.protocols=TLSv1.2 -Dmaven.repo.local=$CI_PROJECT_DIR/.m2/repository -Dorg.slf4j.simpleLogger.log.org.apache.maven.cli.transfer.Slf4jMavenTransferListener=WARN -Dorg.slf4j.simpleLogger.showDateTime=true -Djava.awt.headless=true"
  SONAR_USER_HOME: "${CI_PROJECT_DIR}/.sonar"

stages:
  - test
  - qa

maven_test:
  stage: test
  image: maven:latest
  script:
    - mvn $MAVEN_CLI_OPTS clean verify
  cache:
    paths:
      - .m2/repository
  artifacts:
    paths:
      - target/*
    expire_in: 1 hour
  only:
    - merge_requests

sonarqube_check:
  stage: qa
  image:
    name: sonarsource/sonar-scanner-cli:latest
    entrypoint: [""]
  cache:
    paths:
      - .sonar/cache
  needs:
    - job: maven_test
      artifacts: true
  script:
    - sonar-scanner
      -Dsonar.qualitygate.wait=true
      -Dsonar.projectName=${CI_PROJECT_NAME}
      -Dsonar.projectKey=${CI_PROJECT_NAME}
      -Dsonar.java.binaries=target/classes
      -Dsonar.links.ci=${CI_PROJECT_URL}/pipelines
      -Dsonar.links.homepage=${CI_PROJECT_URL}
      -Dsonar.sourceEncoding=UTF-8
  only:
    - merge_requests

gitleaks:
  stage: qa
  image:
    name: dxa4481/trufflehog:latest
    entrypoint: [""]
  script:
    - >
      trufflehog
      --branch=${CI_COMMIT_BRANCH}
      --since_commit=${CI_COMMIT_BEFORE_SHA}
      --regex
      ${CI_REPOSITORY_URL}
  only:
    - merge_requests
```

#### CI Vars

```
SONAR_HOST_URL
SONAR_TOKEN
```

#### Gitlab config

In `Settings > General > Merge Requests > Merge checks` select `Pipeline must succeed`

### Spring Boot + Docker + Kubernetes

In `.gitlab-ci.yaml`

````yaml
variables:
  MAVEN_OPTS: "-Dhttps.protocols=TLSv1.2 -Dmaven.repo.local=$CI_PROJECT_DIR/.m2/repository -Dorg.slf4j.simpleLogger.log.org.apache.maven.cli.transfer.Slf4jMavenTransferListener=WARN -Dorg.slf4j.simpleLogger.showDateTime=true -Djava.awt.headless=true"

stages:
  - test
  - build
  - containerize
  - deploy

maven test:
  stage: test
  image: maven
  script: mvn $MAVEN_CLI_OPTS clean test
  cache:
    paths:
      - .m2/repository

maven package:
  stage: build
  image: maven
  script: mvn $MAVEN_CLI_OPTS clean package -Dmaven.test.skip=true
  cache:
    paths:
      - .m2/repository
  artifacts:
    paths:
      - target/*.jar
    expire_in: 1 hour

docker containerize:
  stage: containerize
  image:
    name: gcr.io/kaniko-project/executor:debug
    entrypoint: [""]
  script:
    - mkdir -p /kaniko/.docker
    - echo "{\"auths\":{\"$CI_REGISTRY\":{\"username\":\"$CI_REGISTRY_USER\",\"password\":\"$CI_REGISTRY_PASSWORD\"}}}" > /kaniko/.docker/config.json
    - /kaniko/executor --context $CI_PROJECT_DIR --dockerfile $CI_PROJECT_DIR/Dockerfile --destination $CI_REGISTRY_IMAGE:latest

# $CI_COMMIT_TAG

kubernetes deploy:
  stage: deploy
  script: echo 'Deploy'
  when: manual
````

In `Dockerfile`

````dockerfile
FROM adoptopenjdk/openjdk11:jre-11.0.9_11.1-alpine
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/app.jar"]
````

Download image

````
docker login registry.gitlab.com/group -u TOKEN_USER -p TOKEN
docker pull registry.gitlab.com/group/project:latest
docker run -p 8080:8080 registry.gitlab.com/group/project:latest
````

### Trigger other pipeline

```yaml
trigger_job:
    stage: project2_deploy
    script:
    	- “curl -X POST -F token=${OTHER_REPO_TOKEN} -F ref=${REF_NAME} https://gitlab.com/api/v4/projects/2/trigger/pipeline"
    when: on_success
```



## Other sources

https://gitlab.com/gitlab-org/gitlab-ci-yml/tree/master

