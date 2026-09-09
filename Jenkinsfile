pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven to compile and package the code.'
            }
        }      
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit and integration tests with TestNG.'
            }
            post {
                always {
                    emailext(
                        subject: "running test stage build: ${env.BUILD_NUMBER}",
                        body: "The Unit and Integration Tests stage finished with status: ${currentBuild.currentResult}.\n",
                        to: 's223391013@deakin.edu.au',
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analysing code quality and standards using SonarQube.'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scanning for vulnerabilities using OWASP Dependency-Check.'
            }
             post {
                always {
                    emailext (
                        subject: "Security Scan Stage Build: ${env.BUILD_NUMBER}",
                        body: "The Security Scan stage finished with status: ${currentBuild.currentResult}.\n",
                        to: 's223391013@deakin.edu.au',
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to staging AWS EC2 instance.'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests against the staging environment using Postman/Newman.'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying application to production AWS EC2 instance.'
            }
        }
    }
}
