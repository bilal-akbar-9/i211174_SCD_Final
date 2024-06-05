pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        DOCKERHUB_REPO_PREFIX = 'bi1alakbar/scd-final-backend'
        FRONTEND_REPO = 'bi1alakbar/scd-final-frontend'
        IMAGE_TAG = '1'
    }

    stages {
        stage('i211174-Checkout') {
            steps {
                // Checkout the code from GitHub
                sh 'git clone https://github.com/bilal-akbar-9/i211174_SCD_Final.git'
            }
        }

        stage('i211174-Build and Push Auth Image') {
            steps {
                script {
                    echo 'Building and pushing Auth Docker image...'
                    dir('i211174_SCD_Final/Auth') {
                        sh """
                            docker build -t ${DOCKERHUB_REPO_PREFIX}-auth:${IMAGE_TAG} .
                            echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin
                            docker push ${DOCKERHUB_REPO_PREFIX}-auth:${IMAGE_TAG}
                        """
                    }
                }
            }
        }

        stage('i211174-Build and Push Classrooms Image') {
            steps {
                script {
                    echo 'Building and pushing Classrooms Docker image...'
                    dir('i211174_SCD_Final/Classrooms') {
                        sh """
                            docker build -t ${DOCKERHUB_REPO_PREFIX}-classrooms:${IMAGE_TAG} .
                            echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin
                            docker push ${DOCKERHUB_REPO_PREFIX}-classrooms:${IMAGE_TAG}
                        """
                    }
                }
            }
        }

        stage('i211174-Build and Push Event-Bus Image') {
            steps {
                script {
                    echo 'Building and pushing Event-Bus Docker image...'
                    dir('i211174_SCD_Final/event-bus') {
                        sh """
                            docker build -t ${DOCKERHUB_REPO_PREFIX}-event-bus:${IMAGE_TAG} .
                            echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin
                            docker push ${DOCKERHUB_REPO_PREFIX}-event-bus:${IMAGE_TAG}
                        """
                    }
                }
            }
        }

        stage('i211174-Build and Push Post Image') {
            steps {
                script {
                    echo 'Building and pushing Post Docker image...'
                    dir('i211174_SCD_Final/Post') {
                        sh """
                            docker build -t ${DOCKERHUB_REPO_PREFIX}-post:${IMAGE_TAG} .
                            echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin
                            docker push ${DOCKERHUB_REPO_PREFIX}-post:${IMAGE_TAG}
                        """
                    }
                }
            }
        }

        stage('i211174-Build and Push Frontend Image') {
            steps {
                script {
                    echo 'Building and pushing Frontend Docker image...'
                    dir('i211174_SCD_Final/client') {
                        sh """
                            docker build -t ${FRONTEND_REPO}:${IMAGE_TAG} .
                            echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin
                            docker push ${FRONTEND_REPO}:${IMAGE_TAG}
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
