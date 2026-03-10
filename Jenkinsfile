pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/UritiSrikanth/portfolio-devops.git'
            }
        }

        stage('Verify Node Installation') {
            steps {
                sh 'node -v'
                sh 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Stop Old Application') {
            steps {
                sh '''
                    pkill -f "node server.js" || true
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                    nohup node server.js > app.log 2>&1 &
                '''
            }
        }

        stage('Verify Application') {
            steps {
                sh 'sleep 5'
                sh 'netstat -tulnp | grep 3000 || true'
            }
        }

    }

    post {
        success {
            echo 'Pipeline executed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}