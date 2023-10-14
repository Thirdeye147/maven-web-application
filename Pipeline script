pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Build maven') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Thirdeye147/maven-web-application']]])
                    sh 'mvn clean install'
                }
            }
        }
        stage('Build docker image') {
            steps {
                script {
                    sh 'docker build -t thethirdeye147/project . '
                }
            }
        }
        stage('push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'thethirdeye147', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u thethirdeye147 -p ${dockerhubpwd}'
}
                    sh 'docker push thethirdeye147/project '
                }
            }
        }
    }
}


