pipeline {
    agent {
        node {
            label "Dev"
            customWorkspace "/mnt/Docker"
        }
    }
    environment {
    DOCKERHUB_CREDENTIALS = credentials('arpan223')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            rm -rf *
            git clone 'https://github.com/Arpan223/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t arpan/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push arpan/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

