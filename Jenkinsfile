pipeline {
    agent { label 'dockeragent' }

    environment {
        GIT_REPO = 'https://github.com/Anvesh-ansh259/Learn-docker.git'
        BRANCH = 'main'
        IMAGE_NGINX = 'anveshansh259/nginx-app'
        IMAGE_PYTHON = 'anveshansh259/python-app'
        IMAGE_NODE = 'anveshansh259/nodejs-app'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: "${BRANCH}",
                    url: "${GIT_REPO}",
                    credentialsId: 'docker_token'
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub_token', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh """
                            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        """
                    }
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NGINX} ./nginx-app"
                    sh "docker build -t ${IMAGE_PYTHON} ./python-app"
                    sh "docker build -t ${IMAGE_NODE} ./nodejs-app"
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                script {
                    sh "docker push ${IMAGE_NGINX}"
                    sh "docker push ${IMAGE_PYTHON}"
                    sh "docker push ${IMAGE_NODE}"
                    sh "docker logout"
                }
            }
        }
    }

    post {
        success {
            echo "\u2705 Build finished successfully! All stages passed."
        }
        failure {
            echo "\u274C Build failed! Check the logs above for errors."
        }
        always {
            echo 'Pipeline finished.'
        }
    }
}
