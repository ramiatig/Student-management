pipeline {
    agent any

    tools {
        maven 'Maven-3.9.11'  // ton Maven configuré dans Jenkins
        jdk 'JDK17'           // ton JDK configuré dans Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                echo '📥 Récupération du code depuis Git...'
                git branch: 'main', url: 'https://github.com/ramiatig/Student-management.git'
            }
        }

        stage('Pre-Clean') {
            steps {
                echo '🧹 Suppression du dossier target si existant...'
                bat 'if exist target rmdir /s /q target'
            }
        }

        stage('Build & Test') {
            steps {
                echo '🛠 Compilation et tests du projet...'
                bat 'mvn clean install'
            }
        }

        stage('Package & Archive') {
            steps {
                echo '📦 Création du package et archivage...'
                bat 'mvn package'
                archiveArtifacts artifacts: 'target\\*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build terminé avec succès !'
        }
        failure {
            echo '❌ Le build a échoué.'
        }
    }
}
