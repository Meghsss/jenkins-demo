pipeline {
    agent any

    environment {
        VENV_DIR = "venv"
    }

    stages {

        stage('Checkout Code') {
            steps {
                // Checkout the repo
                checkout scm
            }
        }

        stage('Setup Python Environment') {
            steps {
                // Create virtual environment and install dependencies
                sh '''
                python3 -m venv $VENV_DIR
                source $VENV_DIR/bin/activate
                pip install --upgrade pip
                if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
                '''
            }
        }

        stage('Run Script') {
            steps {
                // Run your Python script
                sh '''
                source $VENV_DIR/bin/activate
                python3 hello.py
                '''
            }
        }

        stage('Optional Tests') {
            steps {
                // If you have tests, run them here
                sh '''
                source $VENV_DIR/bin/activate
                if [ -f test_hello.py ]; then python3 -m unittest test_hello.py; fi
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline finished successfully! 🎉"
        }
        failure {
            echo "Pipeline failed! ❌"
        }
    }
}
