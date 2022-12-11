pipeline {
    agent main
    environment {
        DOCKERHUB_CREDENTIALS = credentials('git')
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