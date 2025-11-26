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
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Tests Unitaires') {
            steps {
                echo '🧪 PHASE 3: TEST - Exécution des tests automatisés'
                sh 'mvn test'
            }
        }

    }
}
