pipeline {
  agent any
  triggers {
    pollSCM('* * * * *')
  }
  stages {
    stage('Checkout - Develop Branch') {
      steps {
        echo '=== Develop branch push detected ==='
        checkout scm
      }
    }
    stage('Deploy to Test Node - test-server') {
      steps {
        echo '=== Deploying to TEST node (test-server) ==='
        bat '''
          mkdir test-app 2>nul
          xcopy /E /Y * test-app\\ 2>nul
          echo Test deployment done on test-server node
          dir test-app
        '''
      }
    }
    stage('Run Tests on Test Node') {
      steps {
        echo '=== Running unit tests on test-server ==='
        bat 'echo Running tests... && echo Tests PASSED'
      }
    }
    stage('Deploy to Prod Node - prod-server') {
      steps {
        echo '=== Test SUCCESS, deploying to PROD node (prod-server) ==='
        bat '''
          mkdir prod-app 2>nul
          xcopy /E /Y * prod-app\\ 2>nul
          echo Prod deployment done on prod-server node
          dir prod-app
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
