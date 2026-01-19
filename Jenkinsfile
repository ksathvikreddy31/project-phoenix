pipeline {
    agent any

    tools {
        jdk 'jdk17'
    }

    parameters {
        choice(
            name: 'ENV',
            choices: ['DEV', 'STAGE', 'PROD'],
            description: 'Target environment'
        )
    }

    environment {
        IMAGE_NAME = "phoenix-dosage"
        IMAGE_TAG  = "${env.BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Gradle Build') {
            steps {
                dir('dosage-calculator') {
                    sh './gradlew build'
                }
            }
        }

        stage('Docker Build') {
            steps {
                echo "Building Docker image ${IMAGE_NAME}:${IMAGE_TAG}"
                dir('dosage-calculator') {
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Docker Image Info') {
            steps {
                sh "docker images | grep ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo "Docker image built successfully"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}

