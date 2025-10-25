pipeline {
    agent any

    // ✅ Run only for main or feature/** branches
    when {
        anyOf {
            branch 'main'
            expression { env.BRANCH_NAME ==~ /^feature\/.+$/ }
        }
    }

    stages {
        stage('Setup .NET SDK') {
            steps {
                bat 'dotnet --version'
            }
        }

        stage('Restore Dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
