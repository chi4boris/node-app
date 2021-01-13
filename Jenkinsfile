pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages {
        stage ('Build Docker Image') {
            steps {
                   sh "docker build . -t chi4boris/node-app${DOCKER_TAG}"
            }
        }
        stage('DockerHub Push'){
            steps{
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPwd')]) {
                    sh "docker login -u chi4boris -p ${dockerHubPwd}"
                    sh "docker push chi4boris/nodeapp:${DOCKER_TAG}"
                }
            }
        }   
    }
}

def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}