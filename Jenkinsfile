pipeline {
    agent any

    environment {
        IMAGE_NAME = 'financeme-app'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker rm -f $IMAGE_NAME || true'
                sh 'docker run -d -p 8080:8080 --name $IMAGE_NAME $IMAGE_NAME'
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            cleanWs()
        }
    }
}
