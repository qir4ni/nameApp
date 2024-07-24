pipeline {
    agent any
    environment {
        DOCKER_HOST = 'tcp://localhost:2375/'
        DOCKER_DRIVER = 'overlay2'
    }
    stages {
        stage('Setup Docker') {
            steps {
                script {

                    sh 'apt-get update'
                    sh 'apt-get install -y docker.io'
                    sh 'apt-get install -y docker-compose-plugin'
                    sh 'service docker start'
                    sh 'docker -v'
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'apt-get update'
                    sh 'apt-get install -y docker.io'
                    sh 'apt-get install -y docker-compose-plugin'
                    sh 'service docker start'
                    sh 'docker compose up -d'
                    
                }
            }
        }
        stage('Test') {
            steps {
                script {

                    sh 'apt-get update'
                    sh 'apt-get upgrade -y'
                    sh 'apt-get install -y python3 python3-venv python3-pip'
                    sh 'apt-get install -y docker.io'
                    sh 'service docker start'
     
                    sh 'python3 -m venv /venv'
                    sh 'source /venv/bin/activate'
                    sh 'pip install pytest selenium'
                    

                    sh 'docker compose up -d'
                    

                    sleep 15
                    

                    sh 'python test_devopstest.py'
                }
            }
        }
    }
}
