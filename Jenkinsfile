pipeline {
    agent any

     tools {
        maven 'Maven-3.9.11'      // Nom EXACT de Maven dans Jenkins
        jdk 'JDK17'      // Nom EXACT du JDK dans Jenkins
    }

    environment {
        IMAGE_NAME = "student-management"
        IMAGE_TAG  = "1.0"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ramiatig/Student-management.git'
            }
        }

        stage('Build & Package') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKERHUB_USER',
                    passwordVariable: 'DOCKERHUB_PASS'
                )]) {
                    sh """
                    echo \$DOCKERHUB_PASS | docker login -u \$DOCKERHUB_USER --password-stdin
                    docker tag ${IMAGE_NAME}:${IMAGE_TAG} \$DOCKERHUB_USER/${IMAGE_NAME}:${IMAGE_TAG}
                    docker push \$DOCKERHUB_USER/${IMAGE_NAME}:${IMAGE_TAG}
                    """
                }
            }
        }
    }

    post {
        success { echo '🎉 Image Docker créée et pushée avec succès' }
        failure { echo '❌ Pipeline échoué' }
    }
}
