pipeline{
    agent any
    environment{
        VERSION = "${env.BUILD_ID}"

    }
    stages{
        stage("pull"){
            steps{
                git url: 'https://github.com/Ubaid004/Nodejs-todo-CICD-.git', branch: 'dev'
            }
        }
        stage("build and push"){
            steps{
                withDockerRegistry(credentialsId: 'dockerhubid', url: 'https://registry.hub.docker.com'){
                    sh '''
                       docker build . -t nodejs-todo-cicd:${VERSION}
                       docker tag nodejs-todo-cicd:${VERSION} ubaid004/nodejs-todo-cicd:${VERSION}
                       docker push ubaid004/nodejs-todo-cicd:${VERSION}

                    '''             
                }
            }
        }
        
    }
}

