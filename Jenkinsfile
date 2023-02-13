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
                        docker push nodejs-todo-cicd:${VERSION}
                        docker rmi nodejs-todo-cicd:${VERSION}
                        '''             
                }
            }
        }
        stage("my stage error code 1"){
            steps{
                sh ''' @echo off
                        return_1_if_success.exe   // command which returns 1 in case of success, 0 otherwise
                        IF %ERRORLEVEL% EQU 1 (exit /B 0) ELSE (exit /B 1)'''
            }
        }
    }
}

