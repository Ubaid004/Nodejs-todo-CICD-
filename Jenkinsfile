pipeline{
    agent{ label"Nodejs agent"}
    environment{
        VERSION = "${env.BUILD_ID}"

    }
    stages{
         stage("Nodejs-cicd check"){
            agent {
                docker {
                    image 'node:12.2.0-alpine'
                }
            }
        stage("build and push"){
            steps{
                withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub-passwd')]) {
                        sh '''
                           docker build . -t nodejs-todo-cicd:${VERSION}
                           docker login -u Ubaid004 -p $env.dockerhub-passwd
                           docker push nodejs-todo-cicd:${VERSION}
                           docker rmi nodejs-todo-cicd:${VERSION}
                        '''             
                }
            }
        }
        


    }
}
