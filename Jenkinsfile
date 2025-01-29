pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("flask-demo:4")
                }
            }
        }
        
        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    sh 'docker stop flask-container || true'
                    sh 'docker rm flask-container || true'
            
                    sh 'docker network prune -f'
            
                    sleep 5
            
                    sh 'docker run -d --name flask-container -p 5000:5000 flask-demo:4'
                    )
                }
            }
            stage('Verify') {
                steps {
                    script {
                        sh 'curl --retry 5 --retry-delay 10 http://localhost:5000'
        }
    }
}
        }
    }
    
    post {
        failure {
            echo 'Pipeline failed! Check logs for details.'
        }
    }
}
