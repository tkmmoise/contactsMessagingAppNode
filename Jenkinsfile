pipeline {
    agent any

    stages {
        stage('Init') {
            steps {
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // Assurez-vous que les credentials et l'environnement sont configurés
                sh 'scp -i credentials.pem ./build/package.zip user@server:/path/to/deployment'
            }
        }
    }

    post {
        always {
            mail to: 'dev-team@example.com',
                 subject: "Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
                 body: "Details at ${env.BUILD_URL}"
        }
    }
}
