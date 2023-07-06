pipeline {
    agent any
    environment {
        GIT_URL = 'https://github.com/tikayesi/try-jenkins.git'
        BRANCH = 'tes-pipeline'
        IMAGE = 'my-golang-test'
        CONTAINER = 'my-golang-test-app'
        DOCKER_APP = 'docker'
        DB_HOST = 'product-db'
        DB_USER = 'postgres'
        DB_NAME = 'postgres'
        DB_PASSWORD = 'P@ssw0rd'
        DB_PORT = '5434'
        API_PORT = '8182'
    }
    stages {
        stage("Cleaning up") {
            steps {
                echo 'Cleaning up'
                sh "${DOCKER_APP} rm -f ${CONTAINER} || true"
            }
        }

        stage("Clone") {
            steps {
                echo 'Clone'
                git branch: "${BRANCH}", url: "${GIT_URL}"
            }
        }

        stage("Build and Run") {
            steps {
                echo 'Build and Run'
                sh "DB_HOST=${DB_HOST} DB_PORT=${DB_PORT} DB_NAME=${DB_NAME} DB_USER=${DB_USER} DB_PASSWORD=${DB_PASSWORD} API_PORT=${API_PORT} ${DOCKER_APP} compose up -d"
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
    }
}