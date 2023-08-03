pipeline {
  agent {
    label 'slave-node'
  }
  environment {
    APP_DIR = '/var/www/html/react-app' // Custom application directory
  }
  stages {
    stage('Checkout') {
      steps {
 //       git url: 'https://github.com/your-username/your-nodejs-app.git', branch: 'main', credentialsId: 'correct-git-credentials-id'
	checkout scm
      }
    }
    stage('Build') {
      steps {
        dir(APP_DIR) {
        //  sh 'npm install'
          sh 'npm run build'
        }
      }
    }
  }
}

