pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ml-model"  // Name for your Docker image
        CONTAINER_NAME = "ml-model-container"  // Name for your container
    }

    stages {
        // Clone the Git Repository
        stage('Clone Repository') {
            steps {
                git 'https://github.com/saadbhatti763/ts_exam'  // Replace with your repository URL
            }
        }

        // Build the Docker Image
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE ./src'
            }
        }

        // Deploy using Terraform
        stage('Deploy with Terraform') {
            steps {
                sh '''
                cd terraform
                terraform init
                terraform apply -auto-approve
                '''
            }
        }

        // Test the Deployment
        stage('Test Deployment') {
            steps {
                sh '''
                sleep 10  # Wait for the container to start
                curl -X POST http://localhost:5000/predict -H "Content-Type: application/json" -d '{"features": [1, 2, 3]}'
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Pipeline failed. Check the logs.'
        }
    }
}

