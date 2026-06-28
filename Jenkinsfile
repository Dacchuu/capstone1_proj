pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t capstone-app .'
            }
        }

        stage('Test App Locally') {
            steps {
                echo "Test stage"
            }
        }

        stage('Deploy to Test') {
            steps {
                sh 'ansible-playbook deploy-test.yml'
            }
        }

        stage('Deploy to Prod') {
            steps {
                sh 'ansible-playbook deploy-prod.yml'
            }
        }
    }
}
