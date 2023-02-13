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
                        set +e
                        docker build . -t nodejs-todo-cicd:${VERSION}
                        docker push nodejs-todo-cicd:${VERSION}
                        docker rmi nodejs-todo-cicd:${VERSION}
                        '''             
                }
            }
        }
        
    }
}

