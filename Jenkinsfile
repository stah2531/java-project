properties([pipelineTriggers([githubPush()])])
git credentialsId: 'jenkins-server', url: 'https://github.com/stah2531/java-project.git', branch: 'master' 
pipeline {
   agent any
   stages {
      stage('Unit Tests') {  
         steps {
            
            sh 'ant -f test.xml -v'
            junit 'reports/result.xml'  
         }
      }   
      stage('Build') {   
         steps {
            sh 'ant -f build.xml -v'   
         }
      }   
      stage('Deploy') {    
         steps {
            sh 'aws s3 cp /workspace/java-pipeline/dist/ s3://stah2531-assignment-9/ --recursive --include "rectangle-*.jar"'
         }
      }
      stage('Report') {
         steps {
            withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '2ea2d0a1-0680-4dc9-9381-1bd48028d013', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins" 
            }
         }
      }
   }
}

