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
        echo '🐳 Build image Docker student-management2'
        sh '''
        docker build -t student-management2:1.0 .
        '''
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

                sh "docker tag student-management2:1.0 $DOCKERHUB_USER/student-management2:1.0"

                sh "docker push $DOCKERHUB_USER/student-management2:1.0"
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
