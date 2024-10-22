pipeline {
    agent any
    stages {
        stage('Pull from GitHub') {
            steps {
                git 'https://github.com/abdelkhalek-saadani/tp2-devops.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def appName = 'abdelkhaleksaadanii/spring-and-docker'
                    sh "docker build -t ${appName}:latest ."
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script {
                    def appName = 'abdelkhaleksaadanii/spring-and-docker'
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                        sh "docker push ${appName}:latest"
                    }
                }
            }
        }
    }
}
