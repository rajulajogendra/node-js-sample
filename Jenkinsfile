pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/rakeshragipani/node-js-sample.git'
            }
         }
    stage('Build') {
      steps {
        sh '''
        npm install
        zip -r sample.zip ./*
        
        '''
              }
      }
        }
       }
