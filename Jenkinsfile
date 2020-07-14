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
      stage('lambda')
      steps{
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'ed10dcb8-44af-46dd-90cc-6c368d564a97', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
      sh '''
       aws iam create-role --role-name lambda-ex --assume-role-policy-document file://trust-policy.json
{
    "Role": {
        "Path": "/",
        "RoleName": "lambda-ex",
        "RoleId": "AROAQFOXMPL6TZ6ITKWND",
        "Arn": "arn:aws:iam::123456789012:role/lambda-ex",
        "CreateDate": "2020-01-17T23:19:12Z",
        "AssumeRolePolicyDocument": {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Principal": {
                        "Service": "lambda.amazonaws.com"
                    },
                    "Action": "sts:AssumeRole"
                }
            ]
        }
    }
}
      '''
}
      }
      }
        }
       }
