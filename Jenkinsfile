pipeline {
    agent any
    stages {

        stage('Build') {
            steps {
                echo "Building the war"
            }
        }

        stage("Deploy to QA") {
            steps {
                echo "Deploying to QA"
            }
        }

        stage('Checkout') {
            steps {
                git url: 'https://github.com/revathyj123/Jan2025APIPostmanCollections'
            }
        }

        stage('Pull Docker Image') {
            steps {
                bat 'docker pull jrevathy82/gorestddtest:1.0'
            }
        }

        stage('Run API Test Cases') {
            steps {
                bat 'docker run -v %cd%/newman:/app/results jrevathy82/gorestddtest:1.0'
            }
        }

        stage('Publish HTML Extra Report') {
            steps {
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'newman',
                    reportFiles: 'gorest.html',
                    reportName: 'HTML Extra API Report',
                    reportTitles: ''
                ])
            }
        }

        stage("Deploy to PROD") {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}
