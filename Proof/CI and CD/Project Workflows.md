<h1> Project Workflows </h1>

<h2> Table of Contents </h2>

- [Introduction](#introduction)
	- [What is CI/CD?](#what-is-cicd)
	- [Why do I use it?](#why-do-i-use-it)
	- [Where do I use it?](#where-do-i-use-it)
- [Vue.js Frontend CI](#vuejs-frontend-ci)
- [Java Backend CI](#java-backend-ci)

## Introduction

### What is CI/CD?

CI/CD are processes that developers can implement to reduce the time spent on manually testing code in your project and make it easier for code to be merged and released to the public. Developers can write a CI/CD pipeline, which is usually a bit of yaml code which contains commands which basically prepare the application for production. In a pipeline with only CI, applications are only built and tested (usually unit tests). Pipelines containing CD also have other types of tests, such as acceptance tests and they automatically deploy the application to a staging environment.

For more information about CI/CD, go to [this page](https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment).

### Why do I use it?

I implemented CI/CD into my project repositories, because this automated process saves me a considerable amount of time. I can easily add commands using third party software, which prevents me having to install the software and manually use it (software such as SonarQube/SonarCloud). I also wanted to learn more about how to create a good CI/CD pipeline and be able to explain to others how it works, so that they can also save time. Of course I also wanted to use it, because it's required by my school.

### Where do I use it?

GitHub Actions is used to implement CI/CD into all the repositories of this project. A CI/CD pipeline with GitHub Actions is a workflow that can be present in every repository. Workflows are located in the directory '/.github/workflows'.

## Vue.js Frontend CI

```yml
name: Node.js CI

on:
  push:
  pull_request:
    branches: [ "main", "develop" ]

jobs:
  build_and_test:

    runs-on: ubuntu-latest

    defaults:
      run:
        working-directory: ./vueApp

    strategy:
      matrix:
        node-version: [16.x]

    steps:

    - uses: actions/checkout@v3
      with:
        fetch-depth: 0

    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
        cache-dependency-path: './vueApp/package-lock.json'
        
    - name: Set up application
      run: npm ci
      
    - name: Build application
      run: npm run build --if-present

    - name: Test application
      run: npm test

    - name: SonarCloud Scan
      uses: sonarsource/sonarcloud-github-action@master
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}

  push_to_DockerHub:
    needs: build_and_test
    if: success() && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    
    steps:

    - name: Login to DockerHub
      uses: docker/login-action@v2.0.0
      with:
        username: ${{ secrets.DOCKERHUB_USERNAME }}
        password: ${{ secrets.DOCKERHUB_TOKEN }}

    - name: Build and push Docker images
      uses: docker/build-push-action@v3.1.1
      with:
        push: true
        tags: judahlit/chess_tournament_manager:frontend
```

## Java Backend CI

```yml
name: Java CI with Maven

on:
  push:
    branches: [ "main", "develop" ]
  pull_request:
    branches: [ "main", "develop" ]

jobs:
  build_and_test:
    runs-on: ubuntu-latest

    steps:

    - uses: actions/checkout@v3
      with:
        fetch-depth: 0

    - name: Set up JDK 18
      uses: actions/setup-java@v3
      with:
        java-version: '18'
        distribution: 'temurin'
        cache: maven

    - name: Build and test application
      run: mvn install

    - name: SonarCloud
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
      run: mvn sonar:sonar -Dsonar.host.url="https://sonarcloud.io" -Dsonar.organization=chesstournamentmanager -Dsonar.projectKey=ChessTournamentManager_tournament-svc
  
    - name: Login to DockerHub
      if: success() && github.ref == 'refs/heads/main'
      uses: docker/login-action@v2.0.0
      with:
        username: ${{ secrets.DOCKERHUB_USERNAME }}
        password: ${{ secrets.DOCKERHUB_TOKEN }}

    - name: Build and push Docker images
      if: success() && github.ref == 'refs/heads/main'
      uses: docker/build-push-action@v3.1.1
      with:
        context: .
        push: true
        tags: judahlit/chess_tournament_manager:tournament-svc
```

<h1>Notes:</h1>

For each CI explanation, first post the entire code, then guide the reader through the code using code snippets

- Frontend CI
	- Code
	- Explanation
		- git checkout node blabla
		- build
		- test
		- sonarcloud
		- dockerpush if on main
- Backend CI explanation
	- Code
	- Explanation
		- git checkout node blabla
		- build
		- test
		- sonarcloud
		- dockerpush if on main
- Next Steps