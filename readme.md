# Spring Boot CI/CD Demo Project

This project demonstrates a simple Spring Boot application integrated with a full CI/CD pipeline using **Jenkins**, **GitHub Actions**, **Docker**, and **JUnit Testing**. It is designed to showcase modern DevOps practices in a microservice or monolithic setup.

---

## 📄 Project Structure

```
spring-boot-ci-cd-demo/
├── src/
│   ├── main/java/com/example/demo/
│   │   ├── DemoApplication.java
│   │   └── controller/HelloController.java
│   └── test/java/com/example/demo/
│       └── DemoApplicationTests.java
├── pom.xml
├── Jenkinsfile
├── Dockerfile
├── .github/workflows/maven.yml
└── README.md
```

---

## ⚙️ Technologies Used

* **Java 17**
* **Spring Boot 3.x**
* **Maven**
* **JUnit 5**
* **Jenkins (Declarative Pipeline)**
* **GitHub Actions (CI Workflow)**
* **Docker (Containerization)**

---

## 🚀 API Endpoint

> **GET** `/api/hello`

**Response:**

```json
"Hello from Spring Boot CI/CD!"
```

---

## 📅 Build & Run Locally

### Prerequisites:

* Java 17+
* Maven

### Steps:

```bash
git clone https://github.com/your-username/spring-boot-ci-cd-demo.git
cd spring-boot-ci-cd-demo
mvn clean install
mvn spring-boot:run
```

Open in browser: [http://localhost:8080/api/hello](http://localhost:8080/api/hello)

---

## 🤖 Jenkins Pipeline

A `Jenkinsfile` is included to automate the following stages:

```groovy
pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/spring-boot-ci-cd-demo.git'
            }
        }
        stage('Build') {
            steps { sh 'mvn clean install' }
        }
        stage('Test') {
            steps { sh 'mvn test' }
        }
        stage('Package') {
            steps { sh 'mvn package' }
        }
        stage('Deploy') {
            steps { echo 'Deploying application...' }
        }
    }
    post {
        success { echo 'Build and Deployment Successful!' }
        failure { echo 'Build failed.' }
    }
}
```

> Make sure Jenkins has JDK and Maven installed in **Global Tool Configuration**.

---

## ⚡ GitHub Actions

Located at `.github/workflows/maven.yml`, this workflow auto-triggers on `push` or `pull_request` to `main`:

```yaml
name: Java CI with Maven
on:
  push:
    branches: [ "main" ]
  pull_request:
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
        distribution: 'temurin'
    - name: Build with Maven
      run: mvn clean install
    - name: Run tests
      run: mvn test
```

---

## 🛠️ Docker Support

### Dockerfile

```dockerfile
FROM openjdk:17-jdk-slim
VOLUME /tmp
COPY target/demo-0.0.1-SNAPSHOT.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

### Build & Run:

```bash
mvn clean package -DskipTests
docker build -t springboot-ci-cd .
docker run -p 8080:8080 springboot-ci-cd
```

---

## 📊 Unit Testing

### `DemoApplicationTests.java`

```java
@SpringBootTest
class DemoApplicationTests {
    @Test
    void contextLoads() {}
}
```

> Ensures the Spring context loads properly during CI.

---

## 📚 License

This project is licensed under the MIT License.

---

## 📅 Future Enhancements

* Integration testing with REST-assured
* Docker Compose setup with DB
* Deployment to cloud (AWS, Azure, GCP)
* Add Swagger/OpenAPI documentation

---

## ✨ Author

**Your Name**
[GitHub](https://github.com/your-username) | [LinkedIn](https://linkedin.com/in/your-profile)

---
