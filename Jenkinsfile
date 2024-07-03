node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'SonarScanner';
    withSonarQubeEnv() {
      sh "./sonar-scanner-6.1.0.4477-linux-x64/bin/sonar-scanner"
    }
  }
}
