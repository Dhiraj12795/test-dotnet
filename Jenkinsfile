pipeline {
    agent any
    environment {
        DOTNET_ROOT = tool name: 'dotnet-sdk'
        PATH = "${env.DOTNET_ROOT}/bin:${env.PATH}"
        DEPLOYMENT_PATH = 'Test\DotnetTemplate\DotnetTemplate.csproj'  // Update this path to your actual deployment location
    }
 
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the source repository
                svn 'https://TIPL0031.teleglobal.com/svn/Test'
            }
        }
 
        stage('Restore') {
            steps {
                // Restore dependencies
                sh 'dotnet restore' "Test\DotnetTemplate\DotnetTemplate.csproj"
            }
        }
 
        stage('Build') {
            steps {
                // Build the application
                sh 'dotnet build  Test\DotnetTemplate\DotnetTemplate.csproj --configuration Release'
            }
        }
 
        stage('Test') {
            steps {
                // Run unit tests
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
 
        stage('Publish') {
            steps {
                // Publish the application
                sh 'dotnet publish Test\DotnetTemplate\DotnetTemplate.csproj --configuration Release --output ./publish'
            }
        }
    }
 
    post {
        always {
            // Clean up the workspace after the build
            cleanWs()
        }
    }
}
