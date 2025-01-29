pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build("flask-demo:4")
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh '''
                    docker stop flask-container || true
                    docker rm flask-container || true
                    docker run -d \
                        --name flask-container \
                        -p 5000:5000 \
                        flask-demo:4
                    '''
                }
            }
        }
    }
}
