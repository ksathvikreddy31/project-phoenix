pipeline {
    agent any

    tools {
        jdk 'jdk17'
    }

    parameters {
        choice(
            name: 'ENV',
            choices: ['DEV', 'STAGE', 'PROD'],
            description: 'Select target environment'
        )
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Environment selected: ${params.ENV}"
                echo "Commit: ${env.GIT_COMMIT}"
                echo "Branch: ${env.GIT_BRANCH}"

                dir('dosage-calculator') {
                    sh './gradlew build'
                }
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully'
        }
        failure {
            echo 'Build failed'
        }
    }
}
