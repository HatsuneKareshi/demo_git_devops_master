pipeline {
    agent any

    stages {
        stage('Setup Environment') {
            steps {
                script {
                    echo 'Creating a fresh virtual environment...'
                    // 1. Clean up any old environment to ensure this one is "new"
                    sh 'rm -rf venv' 
                    
                    // 2. Create the virtual environment named "venv"
                    sh 'python3 -m venv venv'
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing pytest...'
                // 3. Install pytest into the virtual environment
                // Note: We use 'venv/bin/pip' to target the environment directly
                sh 'venv/bin/pip install pytest'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running Unit Tests...'
                // 4. Run the specific test file using the environment's pytest
                // This will execute the tests in test_baitap1.py
                sh 'venv/bin/pytest test_baitap1.py'
            }
        }
    }

    // This section runs automatically after the pipeline finishes
    post {
        always {
            echo 'Cleaning up workspace...'
            // 5. Remove the environment to save space and ensure the next build starts fresh
            sh 'rm -rf venv'
        }
    }
}