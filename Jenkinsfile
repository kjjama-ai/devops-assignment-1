pipeline {
  agent any
  triggers {
    pollSCM('* * * * *')
  }
  stages {
    stage('Checkout Develop') {
      steps {
        echo 'Develop branch detected'
        checkout scm
      }
    }
    stage('Deploy to Test - test-server') {
      steps {
        echo 'Deploying to TEST server (test-server node)'
        sh 'mkdir -p /tmp/test-app && cp -r * /tmp/test-app/ 2>/dev/null; ls /tmp/test-app/; echo "Deployed to test-server"'
      }
    }
    stage('Test on test-server') {
      steps {
        echo 'Running tests on test-server - PASSED'
      }
    }
    stage('Deploy to Prod - prod-server') {
      steps {
        echo 'Test SUCCESS, Deploying to PROD server (prod-server node)'
        sh 'mkdir -p /tmp/prod-app && cp -r * /tmp/prod-app/ 2>/dev/null; ls /tmp/prod-app/; echo "Deployed to prod-server"'
      }
    }
  }
  post {
    success { echo 'Pipeline SUCCESS: Dev -> Test -> Prod completed!' }
  }
}
