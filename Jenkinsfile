pipeline {
    agent any // available agent

    stages {
        stage('Checkout the code') {
            //checkout the repository
            steps {
                git branch: 'main', url: 'https://github.com/Dimitrova14/SeleniumWebDriverProject_WithJenkinsPipeline'
            }
        }
        stage('Setup .NET environment') {
            //instal .NET environment
            steps {
                bat '''
                echo Downloading .NET 6.0 SDK
                curl -l -o dotnet-sdk-6.0.132-win-x64.exe https://download.visualstudio.microsoft.com/download/pr/0c82e7e6-fdde-49f2-a69f-bd986aeafe1b/9ea7411a22e661fff0e61e56a466e484/dotnet-sdk-6.0.132-win-x64.exe
                dotnet-sdk-6.0.132-win-x64.exe /quiet/norestart
                '''
                
            }
        }
        stage('Restore nugget packages') {
            //install dependencies
            steps {
                bat 'dotnet restore SeleniumIde.sln'
            }
        }
        stage('Build') {
            //build
            steps {
                bat 'dotnet build SeleniumIde.sln --configuration Release'
            }
        }
        stage('Run Tests') {
            //run tests
            steps {
                bat 'dotnet test SeleniumIde.sln --logger "trx;LogFileName=TestResults.trx"'
            }
        }

        post {
            always {
                archiveArtifacts archive: '**/TestResults/*.trx', allowEmptyArchive: true
                step ([
                    $class: 'MSTestPublisher',
                    testResultsFile: '**/TestResults/*.trx'
                ])
            }
        }
    }
}