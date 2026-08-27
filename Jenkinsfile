pipeline {
    agent any

    parameters {
        choice(name: 'ACTION', choices: ['apply', 'destroy'], description: 'Terraform action')
    }

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rashmigmr13-eng/ec2.git'
            }
        }

        stage('Terraform Init') {
            steps {
                dir('project-1') {
                    sh 'terraform init'
                }
            }
        }

        stage('Terraform Action') {
            steps {
                dir('project-1') {
                    sh """
                        if [ "${params.ACTION}" = "apply" ]; then
                            terraform apply -auto-approve
                        else
                            terraform destroy -auto-approve
                        fi
                    """
                }
            }
        }
    }
}
