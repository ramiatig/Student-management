pipeline {
    agent any

    tools {
        maven "Maven-3.9.11"  
    }

    stages {

        stage('Checkout') {
            steps {
                echo " Récupération du code..."
                git branch: 'main', url: 'https://github.com/ramiatig/Student-management.git'
            }
        }

        stage('Build & Test') {
            steps {
                echo "Build + Tests Maven..."
                bat "mvn clean test"
            }
        }

        stage('Package .jar') {
            steps {
                echo " Packaging du .jar..."
                bat "mvn package -DskipTests"
            }
        }
    }

    post {
        success {
            echo " Pipeline réussie !"
        }
        failure {
            echo " La pipeline a échoué."
        }
    }
}
