pipeline {
    agent any

    // Define custom environment variables
    environment {
        APP_NAME = "MyPythonApp"
        APP_VERSION = "1.2.0"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                // Creates a dummy app.py script so the Build and Deploy stages do not throw an error
                sh '''
                    echo 'print("Hello from ${APP_NAME} version ${APP_VERSION}!")' > app.py
                '''
            }
        }

        stage('Build') {
            steps {
                echo "Running a compile check on app.py using py_compile..."
                // Runs python compilation check
                sh 'python3 -m py_compile app.py'
            }
        }

        stage('Deploy') {
            steps {
                // Pauses and asks for manual user approval
                script {
                    input message: "Approve deployment of ${env.APP_NAME} version ${env.APP_VERSION}?", 
                          ok: "Release"
                }
                
                echo "Deployment approved! Executing app.py..."
                // Runs the script successfully
                sh 'python3 app.py'
            }
        }
    }
}
