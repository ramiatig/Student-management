pipeline {
    agent any

   tools {
        maven 'Maven-3.9.11'
        jdk 'JDK17'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ramiatig/Student-management.git'
            }
        }

        stage('Build') {
            steps {
                // Nettoie l'ancien build et compile le projet
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Exécute les tests unitaires
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Génère le package (jar/war)
                bat 'mvn package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive le jar/war généré pour Jenkins
                archiveArtifacts artifacts: 'target\\*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build terminé avec succès ! 🎉'
        }
        failure {
            echo 'Le build a échoué. ❌'
        }
    }
}
