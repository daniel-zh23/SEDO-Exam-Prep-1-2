pipeline {
    agent any

    environment {
        RUN_FOR_BRANCH = "${env.BRANCH_NAME == 'main' || env.BRANCH_NAME?.startsWith('feature/')}"
    }

    stages {
        stage('Dotnet Version') {
            when {
                expression { return env.RUN_FOR_BRANCH.toBoolean() }
            }
            steps {
                script {
                    bat 'dotnet --version'
                }
            }
        }
        stage('Build Project') {
            when {
                expression { return env.RUN_FOR_BRANCH.toBoolean() }
            }
            steps {
                script {
                    bat 'dotnet build'
                }
            }
        }
        stage('Test project') {
            when {
                expression { return env.RUN_FOR_BRANCH.toBoolean() }
            }
            steps {
                script {
                    bat 'dotnet test --no-build --verbosity normal'
                }
            }
        }

    }

}
