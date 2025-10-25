pipeline {
    agent any


    stages {
        stage('Setup .NET SDK') {
            when { branch pattern: '(main|feature/.*)', comparator: 'REGEXP' }
            steps {
                bat 'dotnet --version'
            }
        }

        stage('Restore Dependencies') {
            when { branch pattern: '(main|feature/.*)', comparator: 'REGEXP' }
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            when { branch pattern: '(main|feature/.*)', comparator: 'REGEXP' }
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            when { branch pattern: '(main|feature/.*)', comparator: 'REGEXP' }
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
