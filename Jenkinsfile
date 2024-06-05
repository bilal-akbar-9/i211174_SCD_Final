pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        DOCKERHUB_REPO_PREFIX = 'bi1alakbar/scd-final-backend'
        FRONTEND_REPO = 'bi1alakbar/scd-final-frontend'
        IMAGE_TAG = '1'
        SERVICES = ['auth', 'classrooms', 'event-bus', 'post', 'frontend']
    }

    stages {
        stage('i211174-Checkout') {
            steps {
                // Checkout the code from GitHub
                sh 'git clone https://github.com/bilal-akbar-9/i211174_SCD_Final.git'
            }
        }

        stage('i211174-Build and Push Docker Images') {
            steps {
                script {
                    for (service in SERVICES) {
                        def imageName = service == 'frontend' ? "${FRONTEND_REPO}:${IMAGE_TAG}" : "${DOCKERHUB_REPO_PREFIX}-${service}:${IMAGE_TAG}"
                        def dockerfilePath = service == 'frontend' ? 'client' : service

                        echo "Building Docker image for ${service}"
                        sh """
                            cd ${dockerfilePath}
                            docker build -t ${imageName} .
                            echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
                            docker push ${imageName}
                        """
                    }
                }
            }
        }
    }

    post {
        always {
            // Clean up the workspace
            cleanWs()
        }
    }
}
