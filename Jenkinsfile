pipeline {
    agent any

    environment {
        // Assurez-vous de remplacer 'SonarQubeServer' par le nom de votre serveur SonarQube configuré dans Jenkins.
        SONARQUBE_SERVER = 'SQserver'
    }

    stages {
        stage('Checkout') {
            steps {
                // Vérifie le code source de votre dépôt SCM (par exemple, Git).
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Compilation du projet avec Maven.
                sh 'mvn clean package'
            }
        }
       
    post {
        success {
            echo 'Build and SonarQube analysis successful.'
        }
        failure {
            echo 'Build or SonarQube analysis failed.'
        }
    }
}
