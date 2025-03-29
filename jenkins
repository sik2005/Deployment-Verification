pipeline {
    agent any  // Runs on any available Jenkins agent

    environment {
        APP_URL = "https://www.sdrbtechnologies.com"  // Replace with your application URL
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', credentialsId: 'git-credentials-id', url: 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building the application..."
                sh './build.sh'  // Replace with actual build command
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying the application..."
                sh './deploy.sh'  // Replace with actual deployment script
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    def response = sh(script: "curl -s -o /dev/null -w '%{http_code}' ${APP_URL}", returnStdout: true).trim()
                    if (response == '200') {
                        echo "✅ Deployment successful!"
                    } else {
                        error "❌ Deployment verification failed! Application not responding."
                    }
                }
            }
        }
    }

    post {
        failure {
            echo "⚠️ Deployment verification failed! Check logs for details."
        }
    }
}
