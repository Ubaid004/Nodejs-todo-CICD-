pipeline{
    agent any
    stages{
        stage("pull"){
            steps{
                git url: 'https://github.com/Ubaid004/Nodejs-todo-CICD-.git', branch: 'dev'
            }
        }
        stage("build"){
            steps{
                script {
                    sh 'docker build . -t nodejs-todo-cicd '
                }
            }
        }
        stage("push"){
            steps{
                script {
                    withCredentials([usernameColonPassword(credentialsId: 'dockerhubid', variable: 'dockerhubCredetials')]){
                        sh '''
                            set +e
                            docker login -u "ubaid004" -p $dockerhubCredetials
                            docker tag nodejs-todo-cicd ubaid004/nodejs-todo-cicd:nodejs-todo-cicd
                            docker push ubaid004/nodejs-todo-cicd
                        '''
                                
                    }
                }
            }
        }
        stage("deploy"){
            steps{
                sh 'docker-compose down'
                sh 'docker-compose up -d --force-recreate --no-deps --build web '
            }
        }
        
    }
}


