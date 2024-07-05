pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout the latest code from the repository
                    git url: 'https://github.com/Madi-art/sonarqube.git', branch: 'main'
                }
            }
        }
        stage('Identify Changed Files') {
            steps {
                script {
                    // Get the list of changed files in the last commit
                    def changedFiles = sh(script: 'git diff-tree --no-commit-id --name-only -r HEAD', returnStdout: true).trim()
                    echo "Changed files: ${changedFiles}"
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}

