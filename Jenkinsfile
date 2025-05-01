pipeline {
    agent {
        docker {
            image 'maven:3.8.6-openjdk-11'
            args '-v /root/.m2:/root/.m2' // Caches Maven dependencies
        }
    }

    environment {
        APP_NAME = "FinanceMe"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
