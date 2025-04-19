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
                cd express-app
                npm install
                node app.js
                '''
      }
    }

    
          }
          
        }