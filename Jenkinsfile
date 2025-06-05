pipeline {
  agent any

  tools {
    nodejs 'default-node' // ชื่อที่คุณตั้งไว้ใน Jenkins
  }

  environment {
    SNYK_TOKEN = credentials('snyk-token')
    STACKHAWK_API_KEY = credentials('stackhawk-api-key')
  }

  stages {
    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Snyk Security Scan') {
      steps {
        sh 'snyk test || true'
      }
    }

    stage('Start App') {
      steps {
        sh 'npm run build'
        sh 'npm start &'
      }
    }

    stage('StackHawk DAST Scan') {
      steps {
        sh 'hawk scan || true'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying...'
      }
    }
  }
}
 