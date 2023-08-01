pipeline {
  agent any
  environment {
    APP_DIR = '/var/www/html/react-app' // Custom application directory
  }
  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/sazalait/react-app.git', branch: 'main', credentialsId: 'your-git-credentials'
      }
    }
    stage('Build') {
      steps {
        dir(APP_DIR) {
          sh 'npm install'
          sh 'npm run build'
        }
      }
    }
  }
}
