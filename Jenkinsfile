pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: env.BRANCH_NAME, url: 'https://github.com/hshar/website.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t webapp:$BUILD_ID .'
            }
        }

        stage('Test App Locally') {
            steps {
                sh 'docker run -d -p 8081:80 --name temp webapp:$BUILD_ID || true'
            }
        }

        stage('Deploy to Test') {
            when {
                branch "develop"
            }
            steps {
                sh 'ansible-playbook deploy-test.yml'
            }
        }

        stage('Deploy to Prod') {
            when {
                branch "master"
            }
            steps {
                sh 'ansible-playbook deploy-prod.yml'
            }
        }
    }
}
