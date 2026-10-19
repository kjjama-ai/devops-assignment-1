pipeline {
  agent any
  stages {
    stage('Checkout from develop') {
      steps {
        echo 'Code from develop branch checked out'
        checkout scm
      }
    }
    stage('Copy to Folder') {
      steps {
        sh '''
          mkdir -p /tmp/myapp
          cp -r * /tmp/myapp/
          echo "Code successfully pulled to /tmp/myapp"
          ls -la /tmp/myapp/
        '''
      }
    }
  }
}
