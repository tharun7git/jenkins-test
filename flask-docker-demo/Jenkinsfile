pipeline {
    agent any

    stages {
        // Stage 1: Checkout code from GitHub
        stage('Checkout') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/tharun7git/jenkins-test.git'
            }
        }

        // Stage 2: Build Docker image
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("flask-demo:${env.BUILD_ID}")
                }
            }
        }

        // Stage 3: Run tests (example)
        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
                // Example: Run pytest if you have tests
                // sh 'docker run flask-demo pytest'
            }
        }

        // Stage 4: Deploy the container
        stage('Deploy') {
            steps {
                script {
                    // Stop old container (if running)
                    sh 'docker stop flask-container || true'
                    sh 'docker rm flask-container || true'
                    
                    // Run new container
                    docker.run(
                        "flask-demo:${env.BUILD_ID}",
                        name: 'flask-container',
                        publishPorts: ['5000:5000'],
                        detach: true
                    )
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful! Access the app at http://localhost:5000'
        }
        failure {
            echo 'Pipeline failed! Check logs for details.'
        }
    }
}
