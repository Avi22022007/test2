pipeline {
    agent any
    
    parameters {
        choice(
            name: 'ENVIRONMENT', 
            choices: ['dev', 'staging', 'prod'], 
            description: 'Select the target environment for deployment'
        )
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code..."
                // In a real pipeline, you would use: checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo "Running compile check on app.py..."
                // Verifies syntax without executing the script
                sh 'python3 -m py_compile app.py'
            }
        }
        
        stage('Deploy') {
            steps {
                // Pause the pipeline for manual approval
                script {
                    input message: "Approve deployment to ${params.ENVIRONMENT}?", ok: "Go"
                }
                
                echo "Deploying to ${params.ENVIRONMENT} environment..."
                sh 'python3 app.py'
            }
        }
    }
}
