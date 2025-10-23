pipeline {
    agent any

    options {
        disableConcurrentBuilds()
        timestamps()
    }

    stages {
        stage('Validate Branch') {
            when {
                expression { env.BRANCH_NAME == 'main' || env.BRANCH_NAME?.startsWith('feature/') }
            }
            steps {
                echo "Branch ${env.BRANCH_NAME} is allowed. Proceeding with build."
            }
        }

        stage('Setup .NET 6') {
            when {
                expression { env.BRANCH_NAME == 'main' || env.BRANCH_NAME?.startsWith('feature/') }
            }
            steps {
                sh 'dotnet --version'
            }
        }

        stage('Restore') {
            when {
                expression { env.BRANCH_NAME == 'main' || env.BRANCH_NAME?.startsWith('feature/') }
            }
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            when {
                expression { env.BRANCH_NAME == 'main' || env.BRANCH_NAME?.startsWith('feature/') }
            }
            steps {
                sh 'dotnet build --configuration Release --no-restore'
            }
        }

        stage('Test') {
            when {
                expression { env.BRANCH_NAME == 'main' || env.BRANCH_NAME?.startsWith('feature/') }
            }
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
