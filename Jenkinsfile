pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/chanhtran235/demo-jenkin.git'
            }
        }

        stage('Build Jar') {
            steps {
                bat 'gradlew.bat clean bootJar'
            }
        }

        stage('Docker Build & Run') {
            steps {
                bat '''
                docker rm -f demo-spring || exit 0
                docker build -t demo-spring .
                docker run -d -p 8088:8088 --name demo-spring demo-spring
                '''
            }
        }
    }

    post {
        success {
            echo '🚀 DEPLOY SUCCESS'
        }
        failure {
            echo '❌ DEPLOY FAILED'
        }
    }
}
