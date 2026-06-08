pipeline{
    agent any

    environment {
            DOCKER_CRED=credentials('dockerhub-creds')
        }
        
    stages{

        stage('Checkout'){
            steps{
                checkout scm
            }
        }
        stage('Build'){
            steps{
                echo 'Building the application...'
                sh 'docker build -t  "$DOCKER_CRED_USR"/app-container .'
            }
        }

        stage('Docker Push') {
            steps {
                sh 'echo "$DOCKER_CRED_PSW" | docker login -u "$DOCKER_CRED_USR" --password-stdin'
                sh 'docker push "$DOCKER_CRED_USR"/app-container'
            }
        }
    }
}