pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('e5be4e22-84d2-4fa8-9706-bd86a2e19dc4')
    }
    stages {
        stage('build') {
            steps {
                sh 'docker build -t sergo92/webapp:v2'
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
    }
}
post {
    always {
        sh 'docker logout'
    }
}