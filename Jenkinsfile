pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('cdobe01')
    }
    stages { 

        stage('Build docker image') {
            steps {  
               
                sh 'docker build -t myapp/flask:$BUILD_NUMBER .'
            }
        }
        stage('Tag docker image') {
            steps {
              
                sh 'docker tag myapp/flask:$BUILD_NUMBER cdobe01/flask:$BUILD_NUMBER'
            }
        }
        stage('Login to DockerHub') {
            steps{
               
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push image') {
            steps{
               
                sh 'docker push cdobe01/flask:$BUILD_NUMBER'
            }
        }
    }
    post {
        always {
           
            sh 'docker logout'
        }
    }
}
