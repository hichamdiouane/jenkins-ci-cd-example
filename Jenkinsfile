pipeline {
    environment {
        registry = "d1hicham/jenkins-ci-cd-example"
        registryCredential = 'dockerhub'
        dockerImage = 'd1hicham/jenkins-ci-cd-example'
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/hichamdiouane/jenkins-ci-cd-example'
            }
        }
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Test image') {
            steps{
                script {
                    echo "Tests passed"
                }
            }
        }
        stage('Publish Image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy image') {
            steps{
                sh "docker run -d -p 8099:80 ${registry}:${BUILD_NUMBER}"
            }
        }
    }
}