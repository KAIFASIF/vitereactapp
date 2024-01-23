pipeline {
    agent any
    
    stages {
        // Stage 1: Checkout code
        stage('checkout') {
            steps {
                // Checkout the code from the specified GitHub repository and branch
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/KAIFASIF/vitereactapp.git']])
            }
        }

        // Stage 2: Build Docker image
        stage('build') {
    steps {
        // Print information about the build environment
        sh 'uname -a'
        sh 'df -h'

        // Build Docker image with the tag 'vitedockerreact'
        sh 'docker build -t vitedockerreact .'
    }
}

// ...

        // Stage 3: Run Docker container on port 3000
        stage('run') {
            steps {
                // Print Docker version for debugging
                sh 'docker version'

                // Print the images available on the host for debugging
                sh 'docker images'

                // Run Docker container with port mapping (host:container)
                sh 'docker run -p 3000:80 -d vitedockerreact'

                // Sleep for a short duration to allow the container to start
                sh 'sleep 10'

                // Print running containers for debugging
                sh 'docker ps'

                // Print container logs for debugging
                sh 'docker logs $(docker ps -q)'
            }
        }
    }
}
