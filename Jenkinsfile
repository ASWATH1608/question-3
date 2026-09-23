pipeline {
    agent any
    environment {
        APP_NAME = "MyPythonApp"
        APP_VERSION = "1.2.0"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                sh '''
                    echo 'print("Hello from ${APP_NAME} version ${APP_VERSION}!")' > app.py
                '''
            }
        }

        stage('Build') {
            steps {
                echo "Running a compile check on app.py using py_compile..."
                sh 'python3 -m py_compile app.py'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    input message: "Approve deployment of ${env.APP_NAME} version ${env.APP_VERSION}?", 
                          ok: "Release"
                }
                echo "Deployment approved! Executing app.py..."
                sh 'python3 app.py'
            }
        }
    }
}
