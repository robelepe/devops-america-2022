pipeline {
    agent { label 'agent2' }
    tools {
        maven 'maven'
    }
    environment {
        registry = "robelepe/nagp-devops-2022"
        registryCredential = 'docker-hub-credential'
        dockerImage = ''
    }
    stages {
        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn clean test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Sonar') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }
        stage('Building Docker') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Push Docker') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}