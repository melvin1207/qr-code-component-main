pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID="374693444425"
        AWS_DEFAULT_REGION="us-east-1"
        IMAGE_REPO_NAME="reto3digital"
        IMAGE_TAG="latest"
        REPOSITORY_URI = "374693444425.dkr.ecr.us-east-1.amazonaws.com/reto3digital"
    }
   
    stages {
        
         stage('Logging into AWS ECR') {
            steps {
                script {
                sh """aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"""
                }
                 
            }
        }
        
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/sd031/aws_codebuild_codedeploy_nodeJs_demo.git']]])     
            }
        }
  
    // Building Docker images
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build "reto3digital:latest"
        }
      }
    }
   
    // Uploading Docker images into AWS ECR
    stage('Pushing to ECR') {
     steps{  
         script {
                sh """docker tag reto3digital:latest 374693444425.dkr.ecr.us-east-1.amazonaws.com/reto3digital:latest"""
                sh """docker push 374693444425.dkr.ecr.us-east-1.amazonaws.com/reto3digital:latest"""
         }
        }
      }
    }
}
