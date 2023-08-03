pipeline {
  agent {
    label 'slave-node'
//    customWorkspace '/var/www/html/react-app'
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
  stage('Run Tests') {
      steps {
	 if (fileExists('package.json') || fileExists('package-lock.json')) {
            // Only run npm install if there are changes
            sh 'npm install'
          } else {
            echo 'No changes in package.json or package-lock.json. Skipping npm install.'
		sh 'npm test'
          }
      }
    }
    stage('Move Files to Project Directory') {
      steps {
        sh "mv /var/www/html/react-app/workspace/react-app/* ${APP_DIR}/"
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

