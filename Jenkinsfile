pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/sumitsonwane31/myflaskapp'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Flask Docker Image..."
                sh 'docker build -t myflaskapp .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                    if [ $(docker ps -aq -f name=myflaskapp) ]; then
                        docker stop myflaskapp || true
                        docker rm myflaskapp || true
                    fi
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name myflaskapp myflaskapp'
            }
        }

        stage('Test Application') {
            steps {
                sh 'curl http://localhost:5000'
            }
        }

        stage('Deploy Success') {
            steps {
                echo 'Deployment completed successfully!'
            }
        }
    }
}
