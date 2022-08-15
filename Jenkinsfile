pipeline {
    agent { label 'test-jenkins-slave' }
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
    }
}