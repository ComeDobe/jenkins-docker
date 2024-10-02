pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('cdobe01')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh 'docker build -f ./Dockerfile -t cdobe01/application:v1.0:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push cdobe01/application:v1.0:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
