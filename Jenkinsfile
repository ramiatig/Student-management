pipeline {
    agent any

    tools {
        // Nom que tu as mis dans Jenkins pour ton JDK 17
        jdk 'JDK-17'
        // Nom que tu as mis dans Jenkins pour Maven
        maven 'Maven-3.9.11'
    }

    stages {
        // ---------------------------
        stage('Checkout Git') {
            steps {
                echo '🎯 PHASE 1: CHECKOUT - Récupération du code source'
                checkout scm
            }
        }

        // ---------------------------
        stage('Build Maven') {
            steps {
                echo '🔨 PHASE 2: BUILD - Compilation du projet Spring Boot'
                // Windows : bat pour exécuter les commandes
                bat 'mvn clean install -DskipTests'
                echo '✅ Compilation terminée et JAR généré dans target/'
            }
        }

        // ---------------------------
        stage('Tests Unitaires') {
            steps {
                echo '🧪 PHASE 3: TEST - Exécution des tests automatisés'
                bat 'mvn test'
                echo '✅ Tests unitaires exécutés et rapports générés dans target/surefire-reports/'
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
