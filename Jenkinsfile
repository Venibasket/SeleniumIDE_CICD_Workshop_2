pipeline {
    agent any

    stages {

        stage('Checkout code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Venibasket/SeleniumIDE_CICD_Workshop_2.git'
            }
        }

        stage ('Set up .NET Core') {
            steps {
                bat '''
                echo Checking .NET SDK installation...
                dotnet --info
                '''
            }
        }

        stage ('Restore dependencies') {
            steps {
                bat '''
                echo Restoring project dependencies...
                dotnet restore SeleniumIde.sln
                '''
            }
        }

        stage ('Build project') {
            steps {
                bat '''
                echo Building the project
                dotnet build
                '''
            }
        }

        stage ('Run tests') {
            steps {
                bat '''
                echo Running tests
                dotnet test SeleniumIde.sln --logger "trx;LogFileName=TestResults.trx"
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.*', allowEmptyArchive: true
        }
    }
}