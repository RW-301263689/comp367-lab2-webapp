pipeline {
    agent any

    tools {
        maven 'MAVEN3'
    }

    environment {
        IMAGE_NAME = 'nero1215/comp367-lab3-webapp:1.0'
        DOCKERHUB_PWD = credentials('dockerhub-pwd')
    }

    stages {
        stage('Check out') {
            steps {
                git branch: 'main', url: 'https://github.com/RuishengWang-301263689/comp367-lab2-webapp.git'
            }
        }

        stage('Build maven project') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker login') {
            steps {
                sh 'echo $DOCKERHUB_PWD | docker login -u nero1215 --password-stdin'
            }
        }

        stage('Docker build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Docker push') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }
    }
}