pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore dependencies') {
            steps {
                echo "Restoring .NET dependencies..."
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                echo "Building .NET project..."
                sh 'dotnet build --no-restore --configuration Debug'
            }
        }

        stage('Run tests') {
            steps {
                echo "Running unit tests..."
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }

    post {
        always {
            echo "Pipeline finished."
        }
    }
}
