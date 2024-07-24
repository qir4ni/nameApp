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

                    sh 'sudo apt-get update'
                    sh 'sudo apt-get install -y docker.io'
                    sh 'sudo service docker start'
                    sh 'docker info'
                }
            }
        }
        stage('Build') {
            steps {
                script {

                    sh 'docker compose up -d'
                    

                    archiveArtifacts artifacts: 'docker-compose.yml'
                }
            }
        }
        stage('Test') {
            steps {
                script {

                    sh 'sudo apt-get update'
                    sh 'sudo apt-get install -y python3 python3-venv python3-pip'
                    
     
                    sh 'python3 -m venv /venv'
                    sh 'source /venv/bin/activate'
                    sh 'pip install pytest selenium'
                    

                    sh 'docker compose up -d'
                    

                    sleep 15
                    
                    // Run the tests
                    sh 'python test_devopstest.py'
                }
            }
        }
    }
}
