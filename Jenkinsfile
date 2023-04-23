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
		    sh "docker rm -f $(sudo docker ps -a -q)"
		}
	}	
      }

        stage('Building Website') {
            steps {
                sh 'docker build /home/ubuntu/IIITV_DEVOPS_CAPSTONE/. -t test'
            }
       }

       stage('Testing Website') {
            steps {
                sh 'echo "Testing Website"'
            }
       }

       stage('Push to Production') {
            steps {
                sh 'docker run -it -p 82:80 -d test'
            }
       }
    }
}
