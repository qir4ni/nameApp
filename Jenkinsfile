pipeline {
    agent any
    environment {
        DOCKER_HOST = 'tcp://localhost:2375/'
        DOCKER_DRIVER = 'overlay2'
    }
    stages {

        stage('Build') {
            steps {
                script {
                    sh 'apt-get update'
                    sh 'apt-get upgrade -y'
                    sh '''
                        curl -L https://github.com/docker/compose/releases/download/v2.29.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
                        chmod +x /usr/local/bin/docker-compose
                        '''
                    sh '''
                        docker-compose version
                        '''
                    
                }
            }
        }
        stage('Test') {
            steps {
                script {

                    sh 'apt-get update'
                    sh 'apt-get upgrade -y'
                    sh '''
                        curl -L https://github.com/docker/compose/releases/download/v2.29.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
                        curl -fsSL https://get.docker.com/ | sh
                        whoami
                        '''
                    sh '''
                        chmod +x /usr/local/bin/docker-compose
                        docker-compose version
                        '''
                    sh 'apt-get install -y python3 python3-venv python3-pip'
                    sh 'service docker start'
     
                    sh 'python3 -m venv /venv'
                    sh 'source /venv/bin/activate'
                    sh 'pip install pytest selenium'
                    

                    sh 'docker-compose up -d'
                    

                    sleep 15
                    

                    sh 'python test_devopstest.py'
                }
            }
        }
    }
}
