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
                        which docker-compose
                        docker-compose version
                        docker compose version
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
                        DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
                        mkdir -p $DOCKER_CONFIG/cli-plugins
                        curl -SL https://github.com/docker/compose/releases/download/v2.29.1/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose
                        '''
                    sh '''
                        chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose
                        docker compose version
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
