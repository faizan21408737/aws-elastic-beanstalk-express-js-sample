pipeline {
    agent {
        // Use Node.js 16 Docker image as the build agent
        docker {
            image 'node:16'
            args '-v $HOME/.npm:/root/.npm' // Mount the npm cache to speed up builds
        }
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install project dependencies
                sh 'npm install --save'
            }
        }

        stage('Build') {
            steps {
                // If there is a build script in package.json, you can run it here
                // Uncomment the line below if applicable
                // sh 'npm run build'
                echo 'Build step (if needed) would be executed here.'
            }
        }

        stage('Test') {
            steps {
                // Run tests (if applicable)
                // Uncomment the line below if you have tests set up
                // sh 'npm test'
                echo 'Test step (if needed) would be executed here.'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy to AWS Elastic Beanstalk or other deployment steps
                echo 'Deployment step would be executed here.'
            }
        }
    }

    post {
        always {
            // Archive the build artifacts (if any)
            archiveArtifacts artifacts: '**/build/**', allowEmptyArchive: true
            
            // Clean up workspace after the build is finished
            cleanWs()
        }
    }
}

