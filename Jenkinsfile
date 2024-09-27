pipeline {
    agent {
        docker {
            image 'node:16'
            args '-v $HOME/.npm:/root/.npm'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing npm dependencies...'
                sh 'npm install --save'
            }
        }

        stage('Install Snyk') {
            steps {
                echo 'Installing Snyk CLI...'
                sh 'npm install -g snyk'
            }
        }

        stage('Authenticate Snyk') {
            steps {
                withCredentials([string(credentialsId: 'snyk-api-token', variable: 'SNYK_TOKEN')]) {
                    sh 'snyk auth $SNYK_TOKEN'
                }
            }
        }

        stage('Security Scan with Snyk') {
            steps {
                echo 'Running Snyk security scan...'
                // Halt the pipeline if critical vulnerabilities are found
                sh 'snyk test --severity-threshold=critical'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                // Add your build steps here
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add your test steps here
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the project...'
                // Add your deployment steps here
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
            cleanWs()
        }
    }
}

