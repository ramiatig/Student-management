pipeline {
    agent any

    tools {
        maven 'Maven-3.9.11'
        jdk 'JDK17'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh "mvn clean package -DskipTests"
            }
        }

        stage('Test') {
            steps {
                sh "mvn test"
            }
        }

        stage('Archive artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Build terminé avec succès 🎉"
        }
        failure {
            echo "Build échoué ❌"
        }
    }
}
pipeline {
    agent any

    tools {
        maven 'Maven-3.9'       // Nom de Maven dans Jenkins (Manage Jenkins > Tools)
        jdk 'JDK17'             // Nom du JDK configuré dans Jenkins
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh "mvn clean package -DskipTests"
            }
        }

        stage('Test') {
            steps {
                sh "mvn test"
            }
        }

        stage('Archive artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Build terminé avec succès 🎉"
        }
        failure {
            echo "Build échoué ❌"
        }
    }
}
