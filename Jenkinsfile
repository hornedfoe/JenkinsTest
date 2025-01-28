pipeline {
    agent any
    
    parameters {
        string(name: 'NAME', defaultValue: 'defaultName', description: 'Enter the name')
        string(name: 'VERSION', defaultValue: '1.0', description: 'Enter the version')
    }
    
    stages {

        stage('Build') {
            steps {
                // Using the parameters in the build steps
                echo "Building... Name: ${params.NAME}, Version: ${params.VERSION}"
            }
        }
        
        stage('Test') {
            steps {
                // Using the parameters in the test steps
                echo "Testing... Name: ${params.NAME}, Version: ${params.VERSION}"
            }
        }
        
        stage('Deploy') {
            steps {
                // Using the parameters in the deploy steps
                echo "Deploying... Name: ${params.NAME}, Version: ${params.VERSION}"
            }
        }
    }
    
    post {
        always {
            // Clean up steps, notifications, etc.
            echo 'Pipeline finished!'
        }
    }
}
