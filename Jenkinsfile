pipeline {
  agent {
    docker {
      image 'mcr.microsoft.com/playwright:v1.43.1-jammy'
      args '--workdir /app -v ${env.WORKSPACE}:/app'
    }
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Install dependencies') {
      steps {
        sh 'npm install'
        sh 'npx playwright install --with-deps'
      }
    }
    stage('Run tests') {
      steps {
        sh 'npx playwright test'
      }
    }
    stage('Archive Test Report') {
      steps {
        archiveArtifacts artifacts: 'playwright-report/**', fingerprint: true
      }
    }
  }
}
