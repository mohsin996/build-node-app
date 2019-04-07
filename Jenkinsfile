pipeline {
  agent any
  stages {
    stage('Create Packer AMI') {
       steps {
            sh 'packer build /packer-ex/build-node-app/packer/packer.json'
        }
      }
    stage('AWS Deployment') {
      steps {
            sh 'rm -rf node-app-terraform'
            sh 'git clone https://github.com/mohsin996/node-app-terraform.git'
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
