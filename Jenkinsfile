pipeline {
    agent any

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
                withCredentials([usernamePassword(credentialsId: 'dockerhub_token', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                }
            }
        }

        stage('Build Nginx Image') {
            steps {
                sh "docker build -t ${IMAGE_NGINX} ./nginx-app"
            }
        }

        stage('Build Python Image') {
            steps {
                sh "docker build -t ${IMAGE_PYTHON} ./python-app"
            }
        }

        stage('Build NodeJS Image') {
            steps {
                sh "docker build -t ${IMAGE_NODE} ./nodejs-app"
            }
        }

        stage('Push Nginx Image') {
            steps {
                sh "docker push ${IMAGE_NGINX}"
            }
        }

        stage('Push Python Image') {
            steps {
                sh "docker push ${IMAGE_PYTHON}"
            }
        }

        stage('Push NodeJS Image') {
            steps {
                sh "docker push ${IMAGE_NODE}"
            }
        }

        stage('Docker Logout') {
            steps {
                sh "docker logout"
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
