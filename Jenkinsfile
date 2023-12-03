pipeline {
    agent any

    stages {
        stage('Application Deployment') {
            agent {
                label 'application'
            }
            steps {
                sh '''
				sudo rm -rf *
    				git clone https://github.com/divyanshu-arya/Priya-project.git/
				cd Priya-project
				docker build -t tomcat .
				docker run -d -p 8080:8080 --name tomcat-server tomcat
				scp -i "Mumbai.pem" init-scripts docker-compose.yml ubuntu@10.0.140.175:/home/ubuntu
				'''
            }
        }
        stage('Database Deployment') {
			agent {
                label 'database'
            }
            steps {
                sh '''
				cd /home/ubuntu/
				docker-compose up --build
				'''
            }
        }
    }
}
