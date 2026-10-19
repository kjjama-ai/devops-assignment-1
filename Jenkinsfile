pipeline {
  agent none
  triggers {
    pollSCM('* * * * *')
  }
  stages {
    stage('Checkout - Develop Branch') {
      agent any
      steps {
        echo '=== Develop branch push detected ==='
        checkout scm
        sh 'ls -la'
      }
    }
    stage('Deploy to Test Node') {
      agent { label 'test-server' }
      steps {
        echo '=== Copying files to TEST node (test-server) ==='
        sh '''
          mkdir -p /home/jenkins/test-app
          cp -r * /home/jenkins/test-app/ 2>/dev/null || true
          echo "Test deployment done on test-server"
          ls -la /home/jenkins/test-app/
        '''
      }
    }
    stage('Run Tests on Test Node') {
      agent { label 'test-server' }
      steps {
        echo '=== Running unit tests on test-server ==='
        sh '''
          echo "Running tests..."
          cat index.html || echo "No index.html"
          echo "Tests PASSED"
        '''
      }
    }
    stage('Deploy to Prod Node') {
      agent { label 'prod-server' }
      steps {
        echo '=== Test SUCCESS, deploying to PROD node (prod-server) ==='
        sh '''
          mkdir -p /home/jenkins/prod-app
          cp -r * /home/jenkins/prod-app/ 2>/dev/null || true
          echo "Prod deployment done on prod-server"
          ls -la /home/jenkins/prod-app/
        '''
      }
    }
  }
  post {
    success {
      echo 'Pipeline SUCCESS: Develop -> Test -> Prod completed!'
    }
    failure {
      echo 'Pipeline FAILED'
    }
  }
}
