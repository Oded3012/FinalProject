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
    stage('Docker Build+TAG') {
        sh 'git clone https://github.com/Oded3012/Infra-Oded.git'
        dir('/var/lib/jenkins/workspace/pipeline-finalp/Infra-Oded') {


        sh 'git checkout main'
        sh 'cp Dockerfile /var/lib/jenkins/workspace/pipeline-finalp'
    }
        sh 'docker build -t hello-world-war:$BUILD_ID .'
  
    }
       
    stage('Push To Nexus Registry') {
        sh 'docker login -u 184.73.211.202:8082'
        sh 'docker tag hello-world-war:$BUILD_ID 184.73.211.202:8082/hello-world:$BUILD_ID'
        sh 'docker push 184.73.211.202:8082/hello-world:$BUILD_ID'
    }
}
