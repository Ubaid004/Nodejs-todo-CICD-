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
                withCredentials([string(credentialsId: 'dockerhubid', variable: 'dockerhubCredetials')]) {
                    sh '''
                       set +e 
                       docker build -t nodejs-todo-cicd:${VERSION} .
                       docker login -u ubaid004 -p $dockerhubCredetials
                       docker push ubaid004/nodejs-todo-cicd:${VERSION}

                    '''                          
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

