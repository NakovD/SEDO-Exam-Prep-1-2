pipeline {
    agent any

    stages {
        stage('Branch Filter') {
            when {
                anyOf {
                    branch 'main'
                    expression { env.BRANCH_NAME ==~ /^feature\/.+$/ }
                }
            }
            steps {
                echo "Branch ${env.BRANCH_NAME} is eligible for build."
            }
        }

        stage('Checkout') {
            when {
                anyOf {
                    branch 'main'
                    expression { env.BRANCH_NAME ==~ /^feature\/.+$/ }
                }
            }
            steps {
                checkout scm
            }
        }

        stage('Setup .NET SDK') {
            when {
                anyOf {
                    branch 'main'
                    expression { env.BRANCH_NAME ==~ /^feature\/.+$/ }
                }
            }
            steps {
                bat 'dotnet --version'
            }
        }

        stage('Restore Dependencies') {
            when {
                anyOf {
                    branch 'main'
                    expression { env.BRANCH_NAME ==~ /^feature\/.+$/ }
                }
            }
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            when {
                anyOf {
                    branch 'main'
                    expression { env.BRANCH_NAME ==~ /^feature\/.+$/ }
                }
            }
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            when {
                anyOf {
                    branch 'main'
                    expression { env.BRANCH_NAME ==~ /^feature\/.+$/ }
                }
            }
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }

    post {
        always {
            echo "Pipeline completed for branch: ${env.BRANCH_NAME}"
        }
        success {
            echo '✅ Build and tests succeeded!'
        }
        failure {
            echo '❌ Build or tests failed.'
        }
    }
}
