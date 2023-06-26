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