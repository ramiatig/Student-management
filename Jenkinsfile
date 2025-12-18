pipeline {
    agent any

    tools {
        maven 'Maven-3.9.11'
        jdk 'JDK17'
    }

    environment {
        IMAGE_NAME = "student-management2"
        IMAGE_TAG  = "1.0"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/ramiatig/Student-management.git'
            }
        }

        stage('Build & Package') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "🐳 Build image Docker ${env.IMAGE_NAME}:${env.IMAGE_TAG}"
                sh "docker build -t ${env.IMAGE_NAME}:${env.IMAGE_TAG} ."
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKERHUB_USER',
                        passwordVariable: 'DOCKERHUB_PASS'
                    )]) {
                        sh "echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin"
                        sh "docker tag ${env.IMAGE_NAME}:${env.IMAGE_TAG} $DOCKERHUB_USER/${env.IMAGE_NAME}:${env.IMAGE_TAG}"
                        sh "docker push $DOCKERHUB_USER/${env.IMAGE_NAME}:${env.IMAGE_TAG}"
                    }
                }
            }
        }
    }

    post {
        success { echo '🎉 Image Docker créée et pushée avec succès' }
        failure { echo '❌ Pipeline échoué' }
    }
}
