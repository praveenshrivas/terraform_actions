pipeline {
    agent any

    environment {
        TF_WORKSPACE = 'default'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "Cloning repository..."
                checkout scm
            }
        }

        stage('Init Terraform') {
            steps {
                sh '''
                    terraform init
                '''
            }
        }

        stage('Validate Terraform') {
            steps {
                sh '''
                    terraform validate
                '''
            }
        }

        stage('Plan Infrastructure') {
            steps {
                sh '''
                    terraform plan -out=tfplan
                '''
            }
        }

        stage('Apply Infrastructure') {
            steps {
                input message: "Proceed with apply?"
                sh '''
                    terraform apply -auto-approve tfplan
                '''
            }
        }
    }

    post {
        always {
            echo "Pipeline completed!"
        }
    }
}
