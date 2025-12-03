    pipeline {
    agent any

   

    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout depuis Git...'
                git branch: 'main', url: 'https://github.com/ramiatig/Student-management.git'
            }
        }

        stage('Build & Test') {
            steps {
                echo ' Build et tests avec Maven...'
                sh "${MVN_HOME}/bin/mvn clean test"
            }
        }

        stage('Package .jar') {
            steps {
                echo ' Création du .jar...'
                sh "${MVN_HOME}/bin/mvn clean package"
            }
        }
    }

    post {
        success {
            echo ' Pipeline terminé avec succès !'
        }
        failure {
            echo ' La pipeline a échoué.'
        }
    }
}
