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
            }
        }
        
        stage('Build') {
            steps {
                echo "Running compile check on app.py..."
                bat 'python -m py_compile app.py'
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    input message: "Approve deployment to ${params.ENVIRONMENT}?", ok: "Go"
                }
                
                echo "Deploying to ${params.ENVIRONMENT} environment..."
                bat 'python app.py'
            }
        }
    }
}
