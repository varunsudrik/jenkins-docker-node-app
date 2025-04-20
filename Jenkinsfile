pipeline {
  agent any

  environment {
    IMAGE_NAME = 'varunsudrik/test-repo'      
    IMAGE_TAG = 'latest'
    REMOTE_USER = 'ubuntu'
    REMOTE_HOST = '3.110.46.206'
    REMOTE_APP_DIR = 'test-jenkins'
    SONAR_PROJECT_KEY = 'test-repo'
    SONAR_SCANNER_HOME = tool 'SonarQubeScanner'         
  }

  stages {
    stage('Checkout') {
      steps {
        git(branch: 'main', url: 'https://github.com/varunsudrik/test-repo.git')
      }
    }

    stage('Install Dependencies') {
      steps {
        sh '''
          cd backend
          npm install
        '''
      }
    }

    stage('SonarQube Analysis') {
      environment {
        SONAR_TOKEN = credentials('sonar-token') // Create this secret in Jenkins
      }
      steps {
        withSonarQubeEnv('My SonarQube Server') {
          sh '''
            cd backend
            ${SONAR_SCANNER_HOME}/bin/sonar-scanner \
              -Dsonar.projectKey=$SONAR_PROJECT_KEY \
              -Dsonar.sources=. \
              -Dsonar.host.url=$SONAR_HOST_URL \
              -Dsonar.login=$SONAR_TOKEN
          '''
        }
      }
    }

    stage('Build Docker Image') {
      steps {
        sh "docker build -t $IMAGE_NAME:$IMAGE_TAG ."
      }
    }

    stage('Push to Docker Hub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          sh '''
            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
            docker push $IMAGE_NAME:$IMAGE_TAG
          '''
        }
      }
    }

    stage('Connect & Deploy on EC2') {
      steps {
        sshagent(['ec2-ssh']) {
          sh """
            ssh -o StrictHostKeyChecking=no $REMOTE_USER@$REMOTE_HOST << EOF
              mkdir -p $REMOTE_APP_DIR
              docker pull $IMAGE_NAME:$IMAGE_TAG
              docker stop test-container || true
              docker rm test-container || true
              docker run -d --name test-container -p 80:3000 $IMAGE_NAME:$IMAGE_TAG
            EOF
          """
        }
      }
    }
  }

  post {
    success {
      echo '✅ CI/CD pipeline executed successfully!'
    }
    failure {
      echo '❌ CI/CD pipeline failed.'
    }
  }
}
