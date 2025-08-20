pipeline {
    agent any
    stages {
        stage('Pull Code') {
            steps {
                git 'https://github.com/Meghsss/jenkins-demo'
            }
        }
        stage('Run Script') {
            steps {
                sh 'python3 hello.py'
            }
        }
    }
}
