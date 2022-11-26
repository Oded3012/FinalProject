pipeline {
  agent any
  stages {
    stage('Checkout Scm') {
      steps {
       git branch: '*/dev-ans', credentialsId: 'git-oded', url: 'https://github.com/Oded3012/hello-world-war.git'
      }
    }
  }
}
