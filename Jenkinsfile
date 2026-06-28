pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                script {
		   sh 'docker build -t capstone.app.'
                }
            }
        }

        stage('Test App Locally') {
            steps {
                echo "Test stage"
            }
        }

        stage('Deploy to Test') {
            when {
                branch 'master'
            }
            steps {
                sh 'ansible-playbook deploy-test.yml'
            }
        }

        stage('Deploy to Prod') {
            when {
                branch 'master'
            }
            steps {
                sh 'ansible-playbook deploy-prod.yml'
            }
        }
    }
}
