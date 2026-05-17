pipeline {
    agent {
        label 'built-in'
    }

    environment {
        IMAGE_NAME = "my-app"
        CONTAINER_NAME = "my-app-container"
        PORT = "8081"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Nareshvj04/jenkins-task2.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Container Operation') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                docker run -d -p $PORT:80 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            emailext(
                subject: "SUCCESS: Job ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                body: """The build was successful!

BUILD SUCCESSFUL!!!

Job: ${env.JOB_NAME}
Build URL: ${env.BUILD_URL}
Build Number: ${env.BUILD_NUMBER}
""",
                to: "nareshvj0402@gmail.com"
            )
        }
    }
}
