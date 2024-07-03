pipeline {
    agent any

    environment {
        // Remplacez 'SonarQubeServer' par le nom de votre serveur SonarQube configuré dans Jenkins.
        SONARQUBE_SERVER = 'SQserver'
        // Ajoutez ici l'URL de votre serveur SonarQube et le token d'authentification.
        SONAR_HOST_URL = 'http://192.168.56.104:9000'
        SONAR_AUTH_TOKEN = 'sqa_3240dc52df9918c0208c65fbcd95c489851cc2e2'
    }

    stages {
        stage('SonarQube analysis') {
            environment {
                // Assurez-vous que votre SonarQube Scanner est configuré.
                SCANNER_HOME = tool name: 'SonarQube Scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
            }
            steps {
                // Analyse SonarQube
                withSonarQubeEnv(SONARQUBE_SERVER) {
                    sh "${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=sonar-jenkins -Dsonar.sources=src -Dsonar.host.url=${SONAR_HOST_URL} -Dsonar.login=${SONAR_AUTH_TOKEN}"
                }
            }
        }

        stage('Quality Gate') {
            steps {
                // Attendre que l'analyse soit complétée et obtenir les résultats du Quality Gate.
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }

    post {
        success {
            echo 'SonarQube analysis successful.'
        }
        failure {
            echo 'SonarQube analysis failed.'
        }
    }
}
