pipeline {
    agent { 
        node { label 'windows' } 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                :: Create venv only if it does not exist
                if not exist venv (
                    python -m venv venv
                )
                :: Activate and install dependencies efficiently
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
        success { echo 'SUCCESS: All stages completed perfectly!' }
        failure { echo 'FAILURE: Something went wrong in the pipeline.' }
    }
}
