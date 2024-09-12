pipeline {
    agent any
    tools {nodejs "node"}

    environment {
        AWS_ACCOUNT_ID="637423480761"
        AWS_DEFAULT_REGION="us-east-1"
        IMAGE_REPO_NAME="jenkins-node-image"
        IMAGE_TAG="latest"
        REPOSITORY_URI = "637423480761.dkr.ecr.us-east-1.amazonaws.com/jenkins-node-image"
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
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/preyeapere/aws-ecr-node-jenkins.git']]])    
            }
        }
 
    // Building Docker images
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build "${IMAGE_REPO_NAME}:${IMAGE_TAG}"
          
        }
      }
    }

    stage('intialising npm installation.......'){
        steps{
            sh 'npm install'
