# Android Docker CI
### Continous Integration (CI) for Android apps
An image for building Android apps.
This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool.
Make sure your CI environment's caching works as expected, this greatly improves the build time, especially if you use multiple build jobs.
Based on [jangrewe/gitlab-ci-android](https://github.com/jangrewe/gitlab-ci-android).

## Setup
1. You need to setup Docker in you machine for generate this Dockerfile into Docker image.
2. You need to publish your Docker image to DockerHub and use it my your self.

## Sample usages
*.gitlab-ci.yml*

```yml
image: you_dockerhub_account/your_docker_image:your_docker_image_tag

before_script:
    - export GRADLE_USER_HOME=`pwd`/.gradle
    - chmod +x ./gradlew

cache:
  key: "$CI_COMMIT_REF_NAME"
  paths:
     - .gradle/

stages:
  - build

build:
  stage: build
  script:
     - ./gradlew assembleDebug
  artifacts:
    paths:
      - app/build/outputs/apk/
```

## Information
For more information, you can read my article [here in medium](https://medium.com/@pahlevikun/simple-step-to-build-an-android-app-with-docker-and-use-in-continuous-integration-d40b54ec8273).
