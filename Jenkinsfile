pipeline {
    agent any 

    environment {
        DOCKER_IMAGE = "arunadocker123/jenkins-demo1"
        DOCKER_TAG = "latest"
        DOCKER_REGISTRY = "docker.io"
        DOCKER_DIGEST = "sha256:a449d2e0b0b2ed78f175d96f41650485ce597400a0db6fb8fd1aa18d5ee282b1"
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building Go Application...'
                sleep 20
            }
        }

        stage('Docker Build & Push') {
            steps {
                echo 'Building and pushing Docker image...'
                sleep 15
            }
        }

        stage('Registering build artifact') {
            steps {
                echo "Registering Docker artifact..."
                script {
                    registerBuildArtifactMetadata(
                        name: "jenkins-demo1",
                        version: "1.0.0",
                        type: "docker",
                        url: "${env.DOCKER_REGISTRY}/${env.DOCKER_IMAGE}:${env.DOCKER_TAG}",
                        digest: "${env.DOCKER_DIGEST}",
                        label: "qa, prod"
                    )
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running Unit Tests...'
                sleep 10
            }
        }

        stage('Deploy') {
            agent any
            steps {
                echo 'Deploying...'
                sleep 10
            }
        }
    }
}
