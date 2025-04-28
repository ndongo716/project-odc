node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'sonar';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
  stage('Cloner le dépôt') {
    steps {
      git branch: 'main',
        url: 'https://github.com/ndongo716/project-odc'
      }
    }
}
