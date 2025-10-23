pipeline {
    agent any

    stages {
        stage('Build and Test') {
            when {
                expression {
                    return env.GIT_BRANCH == 'main' || env.GIT_BRANCH.startsWith('feature/')
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
                        return env.GIT_BRANCH == 'main' || env.GIT_BRANCH.startsWith('feature/')
                    }
                }
            }
            steps {
                echo "⏩ Branch '${env.BRANCH_NAME}' is not allowed (only main or feature/* are built)."
            }
        }
    }

}
