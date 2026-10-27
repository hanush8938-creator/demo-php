pipeline{
    agent any

    enivironment {
        IMAGE_NAME ="hanush8938/php-jenkins-demo"
        CONTAINER_NAME ="php-jenkins-app"
        APP_PORT ="9000"
    }
    stages{
        stage('Checkout'){
            steps{ git branch:'main',url:https:"//github.com/hanush8938-creator/demo-php.git"
            }
           
        }
        stage('build docker image'){
            steps{
                sh ```
                docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} -t $ {IMAGE_NAME}:latest .

                ```
            }
         
        }
        stage('push'){
            steps{
                withCredentials(
                    [usernamePassword(credentialsId:'dockerhub',usernameVariable:'DOCKER_USER',
                    passwordVariable:'DOCKER_TOCKEN')]
                )
            }
        }
        stage('DEPLOY'){
            steps{
                sh ```
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d --name ${CONTAINER_NAME} -p ${APP_PORT}:80 ${IMAGE_NAME}:${BUILD_NUMBER}
                ```
            }
        }
    }
}