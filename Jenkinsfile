pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Krutika-bj/devops-iac-project.git'
            }
        }
        stage('Terraform Init') {
            steps {
                sh '''
                    terraform init
                '''
            }
        }
        stage('Terraform Apply') {
            steps {
                sh '''
                    terraform apply -auto-approve
                '''
            }
        }
        stage('Ansible Provision') {
            steps {
                sh '''
                    ansible-playbook playbook.yml
                '''
            }
        }
        stage('Verify Deployment') {
            steps {
                sh '''
                    curl -f http://localhost:8081 || exit 1
                '''
            }
        }
    }
    post {
        always {
            sh '''
                terraform destroy -auto-approve || true
            '''
        }
    }
}
