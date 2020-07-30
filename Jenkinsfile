pipeline {
   agent any

   stages {
      stage('Github') {
         steps {
            git 'https://github.com/rakeshragipani/node-js-sample.git'
         }
      }
      
      stage('convert to zip') {
         steps{
            sh '''
            npm install 
            zip -r Prodfile.zip ./*
            '''
         }
      }
      
      stage('deploy to lambda') {
          steps{
            withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'ed10dcb8-44af-46dd-90cc-6c368d564a97', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh '''
            aws lambda create-function --function-name Prodlambda  --zip-file fileb://Prodfile.zip --handler index.handler --runtime nodejs12.x  --role arn:aws:iam::246944263478:role/lambdarole --region us-east-1
            
            aws lambda publish-version --function-name Prodlambda --region us-east-1
            VERSION=$(aws lambda publish-version --function-name Prodlambda --region us-east-1 | jq -r .Version)
            aws lambda create-alias --function-name Prodlambda --name Prod --function-version $VERSION --region us-east-1
            '''
         
            }
          }
      }
   }
}

