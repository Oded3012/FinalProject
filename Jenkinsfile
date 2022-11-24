node('built-in') {
    stage('Clean and checkout code') {
        cleanWs()
        checkout([$class: 'GitSCM', branches: [[name: '*/dev-ans']], extensions: [], userRemoteConfigs: [[credentialsId: 'SonarQube', url: 'https://github.com/Oded3012/hello-world-war.git']]])
    }
    stage('SonarQube scan') {
        withSonarQubeEnv(installationName: 'SonarServer') {
            sh 'mvn clean sonar:sonar'
        }
    }
    stage('Build') {
        sh 'mvn compile'
    }
    stage('Test') {
        sh 'mvn test'
    }
    stage('Package') {
        sh 'mvn package'
    }
      stage('Publish artifact') {
       archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
   }
    stage ('Docker Build+TAG') {
       sh 'git clone https://github.com/Oded3012/Infra-Oded.git'
       dir('/opt/tomcat/.jenkins/workspace/Project5-hello-world-war/Infra-Oded') {
       sh 'git checkout Dev'
       sh 'cp Dockerfile /opt/tomcat/.jenkins/workspace/Project5-hello-world-war'
   }
       sh 'docker build -t hello-world-war:$BUILD_ID .'
}
}
