pipeline {
    agent any

    environment {
        APP_NAME = "demo_jekins-0.0.1-SNAPSHOT.jar"
        APP_PORT = "9090"
    }

    stages {
        stage('Checkout Source') {
            steps {
                git branch: 'main', url: 'https://github.com/chanhtran235/demo-jenkin.git'
            }
        }

        stage('Build with Gradle') {
            steps {
                bat '''
                cd %WORKSPACE%
                gradlew.bat clean bootJar
                '''
            }
        }

        stage('Stop Old Application') {
            steps {
                bat '''
                echo Stopping old Spring Boot application if running...
                for /f "tokens=5" %%a in ('netstat -ano ^| findstr :9090') do taskkill /PID %%a /F
                '''
            }
        }

        stage('Run Application') {
            steps {
                bat '''
                echo Starting Spring Boot application on port 9090...
                java -jar build\\libs\\%APP_NAME%
                '''
            }
        }
    }

    post {
        success {
            echo 'Build & Deploy SUCCESSFUL 🎉'
        }
        failure {
            echo 'Build or Deploy FAILED ❌'
        }
    }
}
