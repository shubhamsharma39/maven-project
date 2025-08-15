# Hello Java Maven - Jenkins CI/CD Pipeline

## 📌 Overview
This project is a simple **Java Hello World** application built using **Maven** and integrated with **Jenkins** for CI/CD automation.  
It demonstrates:
- Java application development
- Maven project structure and build
- Packaging into `.jar`
- Automated build and run using Jenkins Pipeline

---

## 🛠️ Project Structure
java-mavan/
├── pom.xml # Maven build configuration file
├── README.md # Project documentation
└── src/
└── main/
└── java/
└── HelloWorld.java # Java source code

---

## ⚙️ Prerequisites
Before running this project, make sure you have:

- **Java JDK 17**
- **Maven 3.6+**
- **Git**
- **Jenkins** (with Maven & JDK configured)

---

## 📂 Source Code
**HelloWorld.java**
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Jenkins + Maven!");
    }
}
📦 Building the Project with Maven
Run the following commands:


# Clone repository
git clone https://github.com/<your-username>/maven-project.git
cd maven-project

# Build using Maven
mvn clean package
After a successful build, you will get:

target/hello-1.0.jar
▶️ Running the Application

java -jar target/hello-1.0.jar
Output:
Hello, Jenkins + Maven!

🏗️ Jenkins Pipeline Setup
1️⃣ Create a New Pipeline Job
Go to Jenkins → New Item → Select Pipeline

Name it hello-java-maven

2️⃣ Pipeline Script (Jenkinsfile)
groovy
Copy code
pipeline {
    agent any
    tools {
        maven 'Maven-3.8.1'
        jdk 'JDK-11'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/shubhamsharma39/maven-project.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Run') {
            steps {
                sh 'java -jar target/hello-1.0.jar'
            }
        }
    }
}
🖥️ Jenkins Pipeline Stages
Checkout

Fetches the latest source code from GitHub.

Build

Runs mvn clean package to compile and package the project into a .jar file.

Run

Executes the generated jar to display output.

⚠️ Common Issues & Fixes
mvn: not found in Jenkins
→ Make sure Maven is installed on Jenkins and configured in Manage Jenkins → Global Tool Configuration.

no main manifest attribute
→ Update pom.xml to include the maven-jar-plugin with Main-Class defined.

Slow build times (~15 min)
→ First build downloads Maven dependencies; subsequent builds will be much faster.


