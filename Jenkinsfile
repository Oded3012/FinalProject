pipeline {
  agent any
  stages {
    stage('Checkout Scm') {
      steps {
       git branch: '*/dev-ans', credentialsId: 'git-oded', url: 'https://github.com/Oded3012/hello-world-war.git'
      }
    }
    stage('Shell script 0') {
      steps {
        sh '''mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=moudle-5 \\
  -Dsonar.host.url=http://192.168.1.243:9000 \\
  -Dsonar.login=sqp_8cb5533d5dd30816f5e4bed51c476b0b1cfd54ee
mvn compile && docker build -t hello_war:${BUILD_ID} .'''
      }
    }
  }
}
