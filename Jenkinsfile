pipeline{
    agent any
    environment{
        dockerimg = "nodejs-todo-cicd"

    }
    stages{
        stage("pull"){
            steps{
                git url: 'https://github.com/Ubaid004/Nodejs-todo-CICD-.git', branch: 'dev'
            }
        }
        stage("build"){
            steps{
                script {
                    DockerImage = docker.build dockerimg
                }
            }
        }
        stage("push"){
            steps{
                script {
                    withCredentials([string(credentialsId: 'dockerhubid', variable: 'dockerhubCredetials')]){
                        sh '''
                            set +e
                            docker login -u "ubaid004" -p $dockerhubCredetials
                        '''
                        DockerImage.push("latest")             
                    }
                }
            }
        }
        stage("deploy"){
            steps{
                sh 'docker-compose down'
                sh 'docker-compose up -d --force-recreate --no-deps --build web'
            }
        }
        
    }
}


