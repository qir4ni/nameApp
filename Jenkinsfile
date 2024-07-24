pipeline {
    agent {
        docker {
            image 'docker:cli'
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        DOCKER_HOST = 'tcp://docker:2375/'
        DOCKER_DRIVER = 'overlay2'
    }
    stages {
        stage('Build') {
            steps {
                script {

                    sh 'docker info'
                    

                    sh 'docker compose up -d'
                    

                }
            }
        }
        stage('Test') {
            steps {
                script {

                    sh 'apt-get update'
                    sh 'apt-get install -y python3 python3-venv python3-pip'
                    

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
