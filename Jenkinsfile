pipeline {
    agent any
    tools {
        maven 'maven' 
    }
    environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
    }
    stages {
        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Build') {
            steps {
                script {
		   docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    	docker.build("tuannguyen03011988/jenkins:${TAG}")
		   }
                }
            }
        }
	    stage('Pushing Docker Image to Dockerhub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        docker.image("tuannguyen03011988/jenkins:${TAG}").push()
                        docker.image("tuannguyen03011988/jenkins:${TAG}").push("latest")
                    }
                }
            }
        }
    }
}
