pipeline {
    agent { 
        label 'ssh_docker'
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub')
    }
    stages {
        stage('build') {
            steps {
                sh 'docker build -t sergo92/webapp:v2 .'
            }
        }
        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push sergo92/webapp:v2'
            }
        }
        stage('Logout') {
            steps {
                sh 'docker logout'
            }
        }
        stage('Roll out new image'){
            steps {
                sh 'cd /home/ansible/'
                sh 'docker pull sergo92/webapp:v2'
                sh 'docker-compose up -d'           
            }
        }
    }
}