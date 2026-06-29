pipeline {
    agent any

    environment {
        VENV_PATH = "${WORKSPACE}/venv"
        PYTHON = "${VENV_PATH}/bin/python"
    }

    stages {
        stage('Setup Environment') {
            steps {
                sh '''#!/bin/bash
                    python3 -m venv venv
                    ${VENV_PATH}/bin/python -m pip install --upgrade pip
                    ${VENV_PATH}/bin/python -m pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '${PYTHON} -m pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Using sh for docker build is often more reliable in simple pipelines
                sh 'docker build -t jenkins_api_build .'
            }
        }
    }
}
