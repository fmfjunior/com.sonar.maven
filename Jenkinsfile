node {

   // This is to demo github action	
   //def sonarUrl = 'sonar.host.url=http://localhost:9000'
   //def mvn = tool (name: 'maven3', type: 'maven') + '/bin/mvn'
   stage('SCM Checkout'){
	deleteDir()
  	checkout scm
    // Clone repo
	//git branch: 'master', 
	//credentialsId: 'github', 
	sh 'git clone https://github.com/fmfjunior/com.sonar.maven'
	//url: 'https://github.com/fmfjunior/com.sonar.maven'
   
   }
   
   stage('Mvn Package'){
	 // Build using maven
	   //Get Maven Home Path
	   def mvnHome = tool name: 'Maven', type: 'maven'
	   sh "${mvnHome}/bin/mvn package"
   }
   
   stage('Sonarqube') {
    environment {
        scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
    }
    steps {
        withSonarQubeEnv('sonarqube') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
    //stage('Sonar Publish'){
	//withCredentials([string(credentialsId: 'sonarqube', variable: 'sonarToken')]) {
        //def sonarToken = "sonar.login=${sonarToken}"
        //sh "${mvn} sonar:sonar -D${sonarUrl}  -D${sonarToken}"
	 //}
      
   //}
   
  // stage('deploy-dev'){
    //   def tomcatDevIp = '172.31.28.172'
	   //def tomcatHome = '/opt/tomcat8/'
	   //def webApps = tomcatHome+'webapps/'
	   //def tomcatStart = "${tomcatHome}bin/startup.sh"
	   //def tomcatStop = "${tomcatHome}bin/shutdown.sh"
	   
	   //sshagent (credentials: ['tomcat-dev']) {
	     // sh "scp -o StrictHostKeyChecking=no target/myweb*.war ec2-user@${tomcatDevIp}:${webApps}myweb.war"
       //   sh "ssh ec2-user@${tomcatDevIp} ${tomcatStop}"
		 // sh "ssh ec2-user@${tomcatDevIp} ${tomcatStart}"
       //}
  // }
  // stage('Email Notification'){
	//	mail bcc: '', body: """Hi Team, You build successfully deployed
	//	                       Job URL : ${env.JOB_URL}
	//						   Job Name: ${env.JOB_NAME}
// Thanks,
// DevOps Team""", cc: '', from: '', replyTo: '', subject: "${env.JOB_NAME} Success", to: 'hari.kammana@gmail.com'
   
   //}
}
