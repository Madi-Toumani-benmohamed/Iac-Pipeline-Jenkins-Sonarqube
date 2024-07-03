pipeline {
    agent any

    environment {
        // Nom du serveur SonarQube configuré dans Jenkins
        SONARQUBE_SERVER = 'SQserver'
        // URL de votre serveur SonarQube
        SONAR_HOST_URL = 'http://192.168.56.104:9000'
        // Jeton d'authentification SonarQube
        SONAR_AUTH_TOKEN = 'sqa_3240dc52df9918c0208c65fbcd95c489851cc2e2'
    }

    stages {
        stage('SonarQube analysis') {
            environment {
                // Utilisez le nom exact de votre installation SonarQube Scanner
                SCANNER_HOME = tool name: 'SonarQubeScanner', type: 'SonarQubeScanner'
            }
            steps {
                script {
                    // Affichez les chemins pour le débogage
                    echo "SonarQube Scanner Home: ${SCANNER_HOME}"
                    echo "SonarQube Server: ${SONARQUBE_SERVER}"
                }

                // Analyse SonarQube
                withSonarQubeEnv(SONARQUBE_SERVER) {
                    sh """
                        ${SCANNER_HOME}/bin/sonar-scanner \
                        -Dsonar.projectKey=sonar-jenkins \
                        -Dsonar.sources=src \
                        -Dsonar.host.url=${SONAR_HOST_URL} \
                        -Dsonar.login=${SONAR_AUTH_TOKEN}
                    """
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
