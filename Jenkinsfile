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
                sh '''
                python3 -m venv venv
                . venv/bin/activate

                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }
        stage('Run Test') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
    
                pytest test_app.py
                ''' 
                
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'docker build  -t rajeev:latest .'
            }
        }
        stage("Run Container") {
            steps {
                sh '''
                    docker stop rajeev || true
                    docker rm rajeev || true
                    docker run -d -p 5000:5000 --name rajeev tanay25/rajeev:latest
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


