pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "sudo docker build . -t iad.ocir.io/idreywyoj0pu/nginx:${DOCKER_TAG} "
            }
        }
        stage('DockerHub Push'){
            steps{
                    sh "sudo docker tag iad.ocir.io/idreywyoj0pu/nginx:${DOCKER_TAG} iad.ocir.io/idreywyoj0pu/nginx:latest"
                    sh "sudo docker push iad.ocir.io/idreywyoj0pu/nginx:latest"
            }
        }
        stage('Deploy to k8s'){
            steps{
                sh "sudo kubectl create -f manifest.yml"

                        
            }
        }  
    }
}


def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
