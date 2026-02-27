# CI-CD-for-Springboot-app.
Project: Spring Boot App with CI/CD using GitHub Actions + Docker + AWS EC2

Step 1: Create a Sample App

Build a simple Spring Boot REST API

Add one endpoint /health

Step 2: Dockerize the App

Create Dockerfile:

FROM openjdk:17
COPY target/app.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]

Build & test:

docker build -t devops-app .
docker run -p 8080:8080 devops-app
Step 3: Push Code to GitHub

Create repository:

devops-cicd-springboot
Step 4: Create GitHub Actions Workflow

.github/workflows/deploy.yml

name: CI-CD Pipeline

on:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          java-version: '17'

      - name: Build
        run: mvn clean package

      - name: Build Docker Image
        run: docker build -t devops-app .


Then configure:

AWS EC2

SSH deployment step
