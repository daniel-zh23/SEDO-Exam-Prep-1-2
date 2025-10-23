pipeline {
    agent any

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

                    bat '''
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

}
