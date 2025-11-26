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
                echo "📦 JAR généré : target/student-management-0.0.1-SNAPSHOT.jar"
            }
        }

        stage('Tests Unitaires') {
            steps {
                echo '🧪 PHASE 3: TEST - Exécution des tests automatisés'
                bat 'mvn test'
                echo "📊 Rapport tests : target/surefire-reports/"
            }
        }

    }
}
