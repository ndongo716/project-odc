pipeline {
    agent any
    
    stages {
        stage('SCM Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    def scannerHome = tool 'sonar'
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
        
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                     url: 'https://github.com/ndongo716/project-odc'
            }
        }
    }
}
