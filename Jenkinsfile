properties([pipelineTriggers([githubPush()])])
node('linux') {
   git credentialsId: 'jenkins-server', url: 'https://github.com/stah2531/java-project.git', branch: 'master'
	stage('Unit Tests') {    
     sh 'ant -f test.xml -v'
     junit 'reports/result.xml'  
	}   

}
