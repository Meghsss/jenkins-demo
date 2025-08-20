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
        echo "it was succesfull, bro!"
    }
    failure {
        echo "oof!, you failed go and check console output for more info!"
    }
}
}