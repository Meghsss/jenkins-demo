pipeline {
    agent any

    environment {
        VENV_DIR = "venv"
    }

    stages {

        stage('Checkout Code') {
            steps {
                // Checkout the repo from GitHub
                checkout scm
            }
        }

        stage('Setup Python Environment') {
            steps {
                // Create virtual environment and install dependencies
                sh '''
                python3 -m venv $VENV_DIR
                $VENV_DIR/bin/pip install --upgrade pip
                if [ -f requirements.txt ]; then $VENV_DIR/bin/pip install -r requirements.txt; fi
                '''
            }
        }

        stage('Run Script') {
            steps {
                // Run your Python script using the virtual environment
                sh '''
                $VENV_DIR/bin/python hello.py
                '''
            }
        }

        stage('Optional Tests') {
            steps {
                // Run tests if test_hello.py exists
                sh '''
                if [ -f test_hello.py ]; then $VENV_DIR/bin/python -m unittest test_hello.py; fi
                '''
            }
        }
    }

    post {
    success {
        mail to: 'youremail@example.com',
             subject: "Jenkins Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
             body: "Good news! The build succeeded."
    }
    failure {
        mail to: 'youremail@example.com',
             subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
             body: "Oops! The build failed. Check Jenkins console for details."
    }
}
}