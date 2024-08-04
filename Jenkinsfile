pipeline {
    agent any // available agent

    stages {
        stage("Checkout the code") {
            //checkout the repository
            steps {
                git branch: 'main', url: 'https://github.com/Dimitrova14/SeleniumWebDriverProject_WithJenkinsPipeline'
            }
        }
        stage("Setup .NET environment") {
            //instal .NET environment
        }
        stage("Restore dependencies") {
            //install dependencies
        }
        stage("Build") {
            //build
        }
        stage("Run Tests") {
            //run tests
        }
    }
}