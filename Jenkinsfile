pipeline {
    tools {
        nodejs 'nodejs'
    }
    agent any
    environment {
        registry = "605134450606.dkr.ecr.eu-north-1.amazonaws.com/alexobsqura/node-app-repo"
    }

    stages {
        
        stage('Building the project') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t repo-jan-2025-api .'
            }
        }
        
        stage('Tag Docker Image') {
            steps {
                sh 'docker tag repo-jan-2025-api:latest 605134450606.dkr.ecr.eu-north-1.amazonaws.com/alexobsqura/node-app-repo:$BUILD_NUMBER'
            }
        }

        stage('Pushing to ECR') {
        steps{  
            script {
                    sh 'aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin 605134450606.dkr.ecr.eu-north-1.amazonaws.com/alexobsqura/node-app-repo'
                    sh 'docker push 605134450606.dkr.ecr.eu-north-1.amazonaws.com/alexobsqura/node-app-repo:$BUILD_NUMBER'
            }
            }
      }
    }
}
