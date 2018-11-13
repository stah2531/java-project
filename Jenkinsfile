properties([pipelineTriggers([githubPush()])])
node('linux') {
   git url: 'https://github.com/stah2531/java-project.git', branch: 'master'
   stage('Unit Tests') { 
      git credentialsId: 'jenkins-server', url: 'https://github.com/stah2531/java-project.git'
   }   
}
