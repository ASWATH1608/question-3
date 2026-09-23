pipeline {
    agent any

    environment {
        APP_NAME = 'MyPythonApp'
        APP_VERSION = '1.2.0'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
            }
        }

        stage('Build') {
            steps {
                echo 'Running a compile check on app.py...'
                sh 'python3 -m py_compile app.py'
            }
        }

        stage('Deploy') {
            steps {
                input message: "Approve deployment of ${env.APP_NAME} version ${env.APP_VERSION}?", ok: "Release"
                
                echo 'Deploying and running application...'
                sh 'python3 app.py'
            }
        }
    }
}
