pipeline {
    agent any

    environment {

        # Optional region (change if needed)
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "📦 Cloning Terraform repository..."
                checkout scm
            }
        }

        stage('Initialize Terraform') {
            steps {
                echo "⚙️ Running terraform init..."
                sh 'terraform init'
            }
        }

        stage('Validate Terraform') {
            steps {
                echo "🔍 Validating Terraform files..."
                sh 'terraform validate'
            }
        }

        stage('Plan Terraform') {
            steps {
                echo "🧠 Planning infrastructure changes..."
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Apply Terraform') {
            steps {
                input message: '🚀 Apply the Terraform plan to AWS?'
                echo "🌍 Applying Terraform changes..."
                sh 'terraform apply -auto-approve tfplan'
            }
        }
    }

    post {
        always {
            echo "✅ Terraform pipeline finished."
        }
    }
}
