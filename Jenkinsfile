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
        stage("build and push"){
            steps{
                withCredentials([string(credentialsId: 'dockerhubid', variable: 'dockerhubCredetials')]) {
                    DockerImage = docker.build dockerimg
                    sh '''
                       set +e
                       docker login -u "ubaid004" -p $dockerhubCredetials
                    '''
                    DockerImage.push("latest")             
                }
            }
        }stage("deploy"){
            steps{
                sh 'docker-compose down'
                sh 'docker-compose up -d --force-recreate --no-deps --build web'
            }
        }
        
    }
}


