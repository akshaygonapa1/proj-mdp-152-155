pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker')
    }
    stages {
        stage('Build docker image') {
            steps {
                sh 'docker build -t akshaygonapa/cal .'
            }   
        }
        stage('login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push  akshaygonapa/cal'
            }
        }
        stage('Remove existing container'){
            steps {
                sh 'docker container rm -f app'

            }
        }
        stage('Run container') {
            steps {
                sh 'docker container run -dt --name app -p 80:8080  akshaygonapa/cal'
                sh 'docker container ls'
            }
        }
    
    }
    
}

