pipeline {
  agent any
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
    stage('Run Test') {
      steps {
        sh '''
                cd backend
                npm run test
                '''
      }
    }

    
          }
          
        }