pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/tanay25/rajeev.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'apt-get update && apt-get install -y python3-pip'
                sh 'pip3 install -r requirements.txt'
            }
        }
        stage('Run Test') {
            steps {
                echo 'Testing...'
                sh 'pytest test_app.py'
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'docker build  -t tanay25/rajeev:latest .'
            }
        }
        stage("Run Container") {
            steps {
                sh '''
                    docker stop tanay25/rajeev || true
                    docker rm tanay25/rajeev || true
                    docker run -d -p 5000:5000 --name tanay25/rajeev tanay25/rajeev:latest
                '''
            }
        }
    }

        post {
            success {
                echo 'Pipeline completed successfully.'
            }
            failure {
                echo 'Pipeline failed.'
            }
        }
    }


