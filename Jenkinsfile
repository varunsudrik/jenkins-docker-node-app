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
    stage('Connect SSH') {
      steps {
        sshagent(['ec2-ssh']) {
    sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.110.46.206 "mkdir -p test-jenkins"'
}

        
      }
    }

    
          }
          
        }