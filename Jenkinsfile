properties([pipelineTriggers([githubPush()])])
node('linux') {
   git credentialsId: 'jenkins-server', url: 'https://github.com/stah2531/java-project.git', branch: 'master'
   stage('Unit Tests') {    
     sh 'ant -f test.xml -v'
     junit 'reports/result.xml'  
   }   
   stage('Build') {    
     sh 'ant -f build.xml -v'   
   }   
   stage('Deploy') {    
     sh 'aws s3 cp /workspace/java-pipeline/dist/ s3://stah2531-assignment-9/ --recursive --include "rectangle-*.jar"'
   }
   stage('Report') {
     sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"   
   }
}
