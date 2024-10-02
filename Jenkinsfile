pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('cdobe01') 
    }
    stages {
        stage('Build docker image') {
            steps {
                script {
                    sh 'docker build -f ./Dockerfile -t cdobe01/application:v1.0.$BUILD_NUMBER .'
                }
            }
        }
        stage('Login to DockerHub') {
            steps {
                script {
                  
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }
        }
        stage('Push docker image') {
            steps {
                script {
                    sh 'docker push cdobe01/application:v1.0.$BUILD_NUMBER'
                }
            }
        }
    }
    post {
        always {
            script {
                sh 'docker logout'
            }
        }
    }
}
