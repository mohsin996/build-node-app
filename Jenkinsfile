pipeline {
  agent {
    docker {
      image 'goforgold/build-container:latest'
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Create Packer AMI') {
        steps {
            sh 'packer build packer/packer.json'
        }
      }
    stage('AWS Deployment') {
      steps {
            sh 'rm -rf node-app-terraform'
            sh 'git clone https://github.com/goforgold/node-app-terraform.git'
            sh '''
               cd node-app-terraform
               terraform init
               terraform apply
            '''
      }
    }
  }
  environment {
    npm_config_cache = 'npm-cache'
 }
}
