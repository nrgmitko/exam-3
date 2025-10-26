pipeline {
        agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore Dependencies') {
            steps {
                echo 'Restoring .NET dependencies...'
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                bat 'dotnet build --configuration Release'
            }
        }

        stage('Run Unit Tests') {
            steps {
                echo 'Running unit tests...'
                bat 'dotnet test --no-build --configuration Release --filter "Category=Unit"'
            }
        }

        stage('Run Integration Tests') {
            steps {
                echo 'Running integration tests...'
                bat 'dotnet test --no-build --configuration Release --filter "Category=Integration"'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
