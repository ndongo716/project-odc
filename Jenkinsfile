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
  stage('Cloner le dépôt') {
    steps {
      git branch: 'main',
        url: 'https://github.com/ndongo716/project-odc'
    }
  }

  stage('Build des images') {
    steps {
      sh "echo helloword"
      sh "docker build -f Backend/dockerfile -t $BACKEND_IMAGE:latest Backend"
      sh "docker build -t $FRONTEND_IMAGE:latest Frontend"
    }
  }

  stage('Push des images sur Docker Hub') {
    steps {
      withDockerRegistry([credentialsId: 'dockerhub', url: '']) {
        sh "docker push $BACKEND_IMAGE:latest"
        sh "docker push $FRONTEND_IMAGE:latest"
      }
    }
  }

  stage('Déploiement local avec Docker Compose') {
    steps {
      sh '''
        docker compose down || exit 0
        docker compose pull
        docker compose up -d --build
      '''
    }
  }
}
