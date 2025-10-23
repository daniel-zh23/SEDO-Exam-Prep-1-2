pipeline {
    agent any

    stages {
        stage('Dotnet Version') {
            when {
                expression {
                    return env.BRANCH_NAME == 'main' || env.BRANCH_NAME?.startsWith('feature/')
                }
            }
            steps {
                script {
                    bat 'dotnet --version'
                }
            }
        }
        stage('Build Project') {
            when {
                expression {
                    return env.BRANCH_NAME == 'main' || env.BRANCH_NAME?.startsWith('feature/')
                }
            }
            steps {
                script {
                    bat 'dotnet build'
                }
            }
        }
        stage('Test project') {
            when {
                expression {
                    return env.BRANCH_NAME == 'main' || env.BRANCH_NAME?.startsWith('feature/')
                }
            }
            steps {
                script {
                    bat 'dotnet test --no-build --verbosity normal'
                }
            }
        }

    }

}
