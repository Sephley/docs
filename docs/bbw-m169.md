# Help for Capture-the-flag Test on 10.07.2023

### gitlab-ci.yml
```
image: docker:23.0.4

variables:
  DOCKER_HOST: tcp://docker:2375
  DOCKER_TLS_CERTDIR: ""

services:
  - docker:23.0.4-dind

package:
  stage: build
  before_script:
    - apk add --no-cache py3-pip
    - pip install awscli
    - aws --version

    - aws ecr get-login-password | docker login --username AWS --password-stdin $CI_AWS_ECR_REGISTRY

  script:
    - docker build --cache-from $CI_AWS_ECR_REGISTRY/$CI_AWS_ECR_REPOSITORY_NAME:latest -t $CI_AWS_ECR_REGISTRY/$CI_AWS_ECR_REPOSITORY_NAME:latest .
    - docker push $CI_AWS_ECR_REGISTRY/$CI_AWS_ECR_REPOSITORY_NAME:latest
```

### Dockerfile
This is an example Dockerfile from the refcard03 Assignment. 
Note that you may need to change some things depending on the application you receive for the test.  
For example the Java version may differ etc.   
```
FROM maven:3-openjdk-11-slim

COPY src /src
COPY pom.xml /
RUN mvn -f pom.xml clean package

RUN mv /target/*.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

It would be better to use a multi-stage version, because time will be crucial during the test.