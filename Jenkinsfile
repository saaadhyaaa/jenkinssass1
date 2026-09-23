pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                if not exist venv (
                    python -m venv venv
                )
                call venv\\Scripts\\activate
                python -m pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat '''
                call venv\\Scripts\\activate
                pytest test_app.py
                '''
            }
        }
    }

    post {
        success { 
            echo 'SUCCESS: All stages completed perfectly!' 
        }
        failure { 
            echo 'FAILURE: Something went wrong in the pipeline.' 
        }
    }
}
