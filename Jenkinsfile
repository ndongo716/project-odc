node {
  environment {
        DOCKER_USER = 'geek120804'
        BACKEND_IMAGE = "${DOCKER_USER}/image-back"
        FRONTEND_IMAGE = "${DOCKER_USER}/image-front"
  }
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'sonar';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
