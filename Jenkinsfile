pipeline {
    agent any
    environment {
	DOCKER_HUB_CREDS = credentials("6185ba91-d961-4d43-8919-5c835b3a777c")
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
                sh 'docker run -it -p 82:80 -d --name capstone_container capstone_image'
            }
       }
    }
}
