pipeline {
    agent { 
        node { 
            label 'windows' // Ensures it runs on your Windows agent
        } 
    }

    stages {
        stage('Checkout') {
            steps {
                // Pulls the latest code from your repository
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                python -m pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat 'pytest test_app.py'
            }
        }
    }

    post {
        success {
            echo '============================================'
            echo 'SUCCESS: All stages completed perfectly!'
            echo '============================================'
        }
        failure {
            echo '============================================'
            echo 'FAILURE: Something went wrong in the pipeline.'
            echo '============================================'
        }
    }
}
