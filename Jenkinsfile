pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/saadbhatti763/402_ts_final_exam.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ml-model ./src'
            }
        }
        stage('Deploy with Terraform') {
            steps {
                sh 'terraform init && terraform apply -auto-approve'
            }
        }
    }
}

