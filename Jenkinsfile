// Powered by Infostretch 

timestamps {

node () {

	stage ('app-ic - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-login', url: 'https://github.com/u161595/jenkins-sample']]]) 
	}
	stage ('app-ic - Build') {
 			// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn clean package " 
			} else { 
 				bat "mvn clean package " 
			} 
 		} 
	}
	stage ('app-ic - Post build actions') {
/*
Please note this is a direct conversion of post-build actions. 
It may not necessarily work/behave in the same way as post-build actions work.
A logic review is suggested.
*/
		// Mailer notification
		step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'jenkins.orsys@gmail.com', sendToIndividuals: false])
 
	}
	
	stage ('app-ic - Quality Analysis') {
		withSonarQubeEnv('Sonar') {
			bat 'mvn sonar:sonar'
		}
	}
}
}
