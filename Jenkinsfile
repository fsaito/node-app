pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "sudo docker build . -t iad.ocir.io/idreywyoj0pu/nodejs:latest"
            }
        }
        stage('OCI Registry Push'){
            steps{
                    sh "sudo docker push iad.ocir.io/idreywyoj0pu/nodejs:latest"
            }
        }
        stage('Deploy to k8s'){
            steps{
                sh "sudo /usr/local/bin/kubectl create -f manifest.yml"

                        
            }
        }  
    }
}


def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
