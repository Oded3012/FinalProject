node('built-in') {
    stage('Clean and checkout code') {
        cleanWs()
        checkout([$class: 'GitSCM', branches: [[name: '*/dev']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-oded', url: 'https://github.com/Oded3012/hello-world-war.git']]])
    }
    stage('SonarQube scan') {
        withSonarQubeEnv(installationName: 'FinalProject-Sonar-Oded') {
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
       dir('/var/lib/jenkins/workspace/pipeline-finalp/Infra-Oded') {
       sh 'git checkout Dev'
       sh 'cp Dockerfile /var/lib/jenkins/workspace/pipeline-finalp'
   }
       sh 'docker build -t hello-world-war:$BUILD_ID .'
}
}
