pipeline {
    agent any

    options {
        disableConcurrentBuilds()
        timestamps()
    }

    environment {
        DOTNET_CLI_TELEMETRY_OPTOUT = '1'
    }

    stages {
        stage('Build and Test') {
            when {
                expression {
                    return env.BRANCH_NAME == 'main' || env.BRANCH_NAME?.startsWith('feature/')
                }
            }
            steps {
                script {
                    echo "✅ Branch ${env.BRANCH_NAME} allowed for build."

                    sh '''
                        echo "Using .NET version:"
                        dotnet --version

                        echo "Restoring..."
                        dotnet restore

                        echo "Building..."
                        dotnet build --configuration Release --no-restore

                        echo "Running tests..."
                        dotnet test --no-build --verbosity normal
                    '''
                }
            }
        }

        stage('Skipped Branch Info') {
            when {
                not {
                    expression {
                        return env.BRANCH_NAME == 'main' || env.BRANCH_NAME?.startsWith('feature/')
                    }
                }
            }
            steps {
                echo "⏩ Branch '${env.BRANCH_NAME}' is not allowed (only main or feature/* are built)."
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline finished successfully for ${env.BRANCH_NAME}"
        }
        failure {
            echo "❌ Pipeline failed for ${env.BRANCH_NAME}"
        }
    }
}
