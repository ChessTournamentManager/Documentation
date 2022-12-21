<h1> Project Workflows </h1>

<h2> Table of Contents </h2>

- [Introduction](#introduction)
  - [What is CI/CD?](#what-is-cicd)
  - [Why do I use it?](#why-do-i-use-it)
  - [Where do I use it?](#where-do-i-use-it)
- [Vue.js Frontend CI](#vuejs-frontend-ci)
- [Java Backend CI](#java-backend-ci)
- [Next Steps](#next-steps)

## Introduction

### What is CI/CD?

CI/CD are processes that developers can implement to reduce the time spent on manually testing code in your project and make it easier for code to be merged and released to the public. Developers can write a CI/CD pipeline, which is usually a bit of yaml code which contains commands which basically prepare the application for production. In a pipeline with only CI, applications are only built and tested (usually unit tests). Pipelines containing CD also have other types of tests, such as acceptance tests and they automatically deploy the application to a staging environment.

For more information about CI/CD, go to [this page](https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment).

### Why do I use it?

I implemented CI/CD into my project repositories, because this automated process saves me a considerable amount of time. Without a CI/CD pipeline, this is what the developer process would look like every time some code should be merged with the main or develop branch:

1. The developer would have to run a command which would build the application, to make sure there are no errors.
2. The developer would have to run a command which would run the tests and make sure they pass.

This would be very annoying to do every single time. You could also forget to do it, which could result in faulty code being merged to important branches, which would be time-consuming to fix. However, this process would be even more time-consuming and fault-prone if you want to use third party software to look at your code, or if you want to deploy your application, or if you want to run different types of tests with different commands:

1. The developer would have to run a command which would build the application, to make sure there are no errors.
2. The developer would have to run a command which would run the unit tests and make sure they pass.
3. The developer would have to run a command which would run the integration tests and make sure they pass.
4. The developer would have to run a command which would run the performance tests and make sure they pass.
5. The developer would have to run a command (or multiple commands) which would make third party software scan the code in the project for vulnerabilities, bugs, etc. If these results should be available online, the developer must pass in a token every single time.
6. The developer would have to run commands which would deploy this application to a cloud service. For this step, the developer needs to be certain that all the other steps have already been done, otherwise faulty code would be present in the production environment!

As you can see, this process would be much more time-consuming if it wasn't automated with a pipeline. It is also much more likely for something to go wrong, because the developer could easily forget to do something when merging code to an important branch. This is why it is objectivly better to use CI/CD. It is important for me, as a professional software developer, to choose the best methods and tools available, so I can continually improve my skills.

It is also very easy to add third party software into a CI/CD pipeline (software such as SonarQube/SonarCloud). This kind of software increases the quality assurance of my code, by scanning it for vulnerabilities, bugs, code smells and more. I also wanted to learn more about how to create a good CI/CD pipeline and be able to explain to others how it works, so that they can also save time.

### Where do I use it?

GitHub Actions is used to implement CI/CD into all the repositories of this project. A CI/CD pipeline with GitHub Actions is a workflow that can be present in every repository. Workflows are located in the directory '/.github/workflows'.

## Vue.js Frontend CI

This is the complete workflow that I use for the frontend:

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

In this part of the workflow, I tell GitHub to only run it when I have made a push or when I have requested a pull request to the develop or master branch:

```yml
on:
  push:
  pull_request:
    branches: [ "main", "develop" ]
```

Then I make some preparations before I actually build and test my application. I first tell GitHub to run my application on ubuntu and to go into the 'vueApp' directory:

```yml
    runs-on: ubuntu-latest

    defaults:
      run:
        working-directory: ./vueApp
```

After that, I tell GitHub to install node.js. This will make it possible to run the commands I will use later. I could also install multiple versions of node here and make the workflow run multiple times. I choose not to do that, because that is inconvenient when I want to run checks with SonarCLoud (this will be seen later).

```yml
    strategy:
      matrix:
        node-version: [16.x]
```

I then use a GitHub action which checks-out my repository under the $GITHUB_WORKSPACE, so the workflow can access it. I also get the whole branch with its entire history, which is something SonarCloud wants to have.

```yml
    steps:

    - uses: actions/checkout@v3
      with:
        fetch-depth: 0
```

After that, a GitHub action is used to setup Node.js for the workflow. When that is completed, the node dependencies that the application needs are installed. The application is now ready to be built and tested.

```yml
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
        cache-dependency-path: './vueApp/package-lock.json'
        
    - name: Set up application
      run: npm ci
```

Then the workflow tells GitHub to build the application and run all the tests:

```yml      
    - name: Build application
      run: npm run build --if-present

    - name: Test application
      run: npm test
```

After that, SonarCloud will analyze the application to see whether there are bugs, vulnerabilities, etc. The tokens that I use are stored as secrets in Github. I refer to those secrets in the workflow:

```yml
    - name: SonarCloud Scan
      uses: sonarsource/sonarcloud-github-action@master
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```

In the next Job, I will push the application to Dockerhub. In this first part, I only let this job be executed if the workflow has run successfully so far and if the branch which the workflow is running on is the master branch:

```yml
  push_to_DockerHub:
    needs: build_and_test
    if: success() && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
```

In here, I log into Dockerhub with a GitHub action by using my credentials which I saved as GitHub secrets:

```yml
    steps:

    - name: Login to DockerHub
      uses: docker/login-action@v2.0.0
      with:
        username: ${{ secrets.DOCKERHUB_USERNAME }}
        password: ${{ secrets.DOCKERHUB_TOKEN }}
```

And lastly, I push my application to DockerHub in the chess_tournament_manager repository as a docker image tagged as 'frontend'.

```yml
    - name: Build and push Docker images
      uses: docker/build-push-action@v3.1.1
      with:
        push: true
        tags: judahlit/chess_tournament_manager:frontend
```


## Java Backend CI

This is the workflow that I use for the backend services. This workflow is very similar to the frontend workflow, so I won't explain it step by step. The only differences here, is that the workflow doesn't trigger on every push and that Maven is used instead of Node.js.

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

## Next Steps

Now that I have working workflows, I can now monitor more easily whether my application works as intended or not. The next steps are to add good tests and to keep an eye on the SonarCloud analyses of each of my components.