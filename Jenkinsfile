node {
    stage('SCM Checkout') {
        checkout scm
    }
    
    stage('SonarQube Analysis') {
        def scannerHome = tool 'sonar'
        withSonarQubeEnv('SonarQube') {  // Specify your SonarQube server name
            sh "${scannerHome}/bin/sonar-scanner"
        }
    }
    
    stage('Clone Repository') {
        git branch: 'main',
             url: 'https://github.com/ndongo716/project-odc'
    }
}
