pipeline {
    agent any
    stages {
        stage('Validate Branch') {
            when {
                expression {
                    env.BRANCH_NAME == 'main' || env.BRANCH_NAME.startsWith('feature/')
                }
            }
        }
        stages {
        stage('Setup .NET 6') {
            steps {
                sh 'dotnet --version'
            }
        }

        stage('Restore') {
            steps {
                echo "Restoring NuGet packages"
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                echo "Building the project"
                sh 'dotnet build --configuration Release --no-restore'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests"
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
        }
    }
}