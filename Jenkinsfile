pipeline {
  agent any

  environment {
    PM2_HOME = '/home/ubuntu/.pm2' // Adjust this path based on your user
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/mihindu-innovo/jenkins-test-nest.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }

    stage('Test') {
      steps {
        sh 'npm run test'
      }
    }

    stage('Deploy with PM2') {
      steps {
        // Stop the application if it's already running
        sh 'sudo pm2 stop jenkins-test-nest || true'

        // Start the application with PM2
        sh 'sudo pm2 start dist/main.js --name jenkins-test-nest'

        // Save the PM2 process list to restart after reboot
        sh 'sudo pm2 save'
      }
    }
  }

  post {
    success {
      echo 'Application deployed successfully with PM2'
    }
    failure {
      echo 'Deployment failed'
    }
  }
}

