pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Build Jar') {
            steps {
                sh "mvn clean package -DskipTests"
            }
        }
        stage('Build Image') {
            steps {
                sh "docker build -t='mdabdulawal/selenium-docker' ."
            }
        }
        stage('Push Image') {
            steps {
			    withCredentials([usernamePassword(credentialsId: 'awaldocker', passwordVariable: 'pass', usernameVariable: 'user')]) {
			        sh "docker login --username=mdabdulawal --password=seleniumDocker"
			        sh "docker push mdabdulawal/selenium-docker:latest"
			    }                           
            }
        }
    }
}