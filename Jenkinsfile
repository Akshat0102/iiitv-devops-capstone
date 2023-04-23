pipeline {
    agent any
    environment {
	DOCKER_HUB_CREDS = credentials("202051016_capstone")
    }
    stages {
	stage('Login to dockerhub') {
	   steps {
		script {
		    sh "docker login -u ${DOCKER_HUB_CREDS_USR} -p ${DOCKER_HUB_CREDS_PSW}"
		}
	}	
     }
	stage('Remove existing container if any') {
            steps {
                script {
		    try {
			sh "docker rm -f capstone_container"
		   } catch (e) {
			sh 'echo "Container does not exist"'	
		}
                }
        }       
      }
        stage('Building Website') {
            steps {
                sh 'docker build . -t capstone_image'
            }
       }

       stage('Testing Website') {
            steps {
                sh 'echo "Testing Website"'
            }
       }

       stage('Push to Production') {
            steps {
                sh 'docker run -it -p 82:80 -d --name 202051016_container 202051016_image'
            }
       }
    }
}
