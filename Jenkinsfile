pipeline {
    agent any

    stages {
	stage('Remove existing container if any') {
	    steps {
	       sh 'sudo docker rm -f $(sudo docker ps -a -q)'  
	   }
      }
        stage('Building Website') {
            steps {
                sh 'sudo docker build /home/ubuntu/IIITV_DEVOPS_CAPSTONE/. -t test'
            }
       }

       stage('Testing Website') {
            steps {
                sh 'echo "Testing Website"'
            }
       }

       stage('Push to Production') {
            steps {
                sh 'sudo docker run -it -p 82:80 -d test'
            }
       }
    }
}
