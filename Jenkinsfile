pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    environment {
        // Nom du serveur SonarQube configuré dans Jenkins
        SONARQUBE_SERVER = 'SQserver'
        // URL de votre serveur SonarQube
        SONAR_HOST_URL = 'http://192.168.56.104:9000'
        // Jeton d'authentification SonarQube
        SONAR_AUTH_TOKEN = 'sqa_3240dc52df9918c0208c65fbcd95c489851cc2e2'
    }

    stages {
        stage('SCM') {
            steps {
                // Vérifie le code source de votre dépôt SCM (par exemple, Git)
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Utilisation d'un outil configuré dans Jenkins
                 //   def scannerHome = tool 'SonarScanner'
                    
                    // Exécution du scanner
                    withSonarQubeEnv('SQserver') {
                        sh """
                            pwd \
                            ./sonar-scanner-6.1.0.4477-linux-x64/bin/sonar-scanner \
                            -Dsonar.projectKey=sonar-jenkins \
                            -Dsonar.sources=src \
                            -Dsonar.host.url=${SONAR_HOST_URL} \
                            -Dsonar.login=${SONAR_AUTH_TOKEN}
                        """
                    }
                }
            }
        }

        stage('Quality Gate') {
            steps {
                // Attendre que l'analyse soit complétée et obtenir les résultats du Quality Gate
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
