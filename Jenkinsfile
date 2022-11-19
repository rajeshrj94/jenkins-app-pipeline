//Declarative Pipeline
def VERSION='1.0.0'
pipeline {
    agent none
    environment {
        PROJECT = "WELCOME TO Java Sample Application"
    }
    stages {
        stage("Tools initialization") {
            agent { label 'DEV' }
            steps {
                sh "mvn --version"
                sh "java -version"
            }
        }
        stage('mvn clean') {
            agent { label 'DEV' }
            steps { 
                sh "mvn clean"
            }
        }
        stage('mvn test') {
            agent { label 'DEV' }
            steps { 
                sh "mvn test"
            }
        }
        stage('mvn package') {
            agent { label 'DEV' }
            steps { 
                sh "mvn package"
            }
        }
        stage('docker build') {
            agent { label 'DEV' }
            steps { 
                sh "sudo docker build -t rajeshrj94/devspring:$BUILD_NUMBER ."
            }
        }
        stage('Deploy Docker Image') {
            agent { label 'DEV' }
            steps { 
                sh "sudo docker stop springbootapp || sudo docker ps"
                sh "sudo docker run --rm -dit --name springbootapp -p 8080:8080 rajeshrj94/devspring:$BUILD_NUMBER"
            }
        }
    }
}


