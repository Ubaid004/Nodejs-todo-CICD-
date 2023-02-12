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
                withCredentials([string(credentialsId: 'dockerhub-passwd', variable: 'dockerhub-passwd')]) {
                        sh '''
                           docker build . -t nodejs-todo-cicd:${VERSION}
                           docker login -u Ubaid004 -p ${dockerhub-passwd}
                           docker push nodejs-todo-cicd:${VERSION}
                           docker rmi nodejs-todo-cicd:${VERSION}
                        '''             
                }
            }
        }
        
    }
}
