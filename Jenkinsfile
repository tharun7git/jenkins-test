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
                    docker run --name flask-container -p 5050:5050 flask-demo:4
                    '''
                }
            }
        }
    }
}
