pipeline {
    agent any

    stages {
        stage('Checkout Git') {
            steps {
                echo '🎯 PHASE 1: CHECKOUT - Récupération du code source'
                checkout scm
            }
        }

        stage('Build Maven') {
            steps {
                echo '🔨 PHASE 2: BUILD - Compilation du projet Spring Boot'
                bat 'mvn clean install -DskipTests'
            }
        }

        stage('Tests Unitaires') {
            steps {
                echo '🧪 PHASE 3: TEST - Exécution des tests unitaires'
                bat 'mvn test'
            }
        }
    }

    post {
        success {
            echo '🎉 Pipeline terminé avec succès !'
        }
        failure {
            echo '❌ Pipeline échoué. Vérifie les erreurs ci-dessus.'
        }
    }
}
