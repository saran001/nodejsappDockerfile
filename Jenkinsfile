pipeline {
    agent any
    stages {
        stage('Clone my Source Code') {
            steps {
                git 'https://github.com/saran001/nodejsappDockerfile.git'
            }
        }
        stage('Build and Push') {
            steps {
                script {
                    try {
                        docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                            def customImage = docker.build("sarandev001/nodejsapp:${env.BUILD_NUMBER}.0")
                            /* Push the container to the Docker Hub Registry */
                            customImage.push()
                        }
                    } catch (Exception e) {
                        error "Build or push failed: ${e.message}"
                    }
                }
            }
            post {
                success {
                    echo 'Image successfully built and pushed!!!'
                }
                failure {
                    echo 'Build or push failed.'
                }
            }
        }
    }
}
