pipeline {
  agent any
  environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "localhost:8081"
        NEXUS_REPOSITORY = "Sample_Mobile_Application"
        NEXUS_CREDENTIAL_ID = "Nexus_ID"
    }
  stages {	
	stage('Checkout'){
		checkout(
	}
	stage('Build'){
		steps{
			bat 'mvn compile'
	       	}
	}
	
	stage('Unit Test') {
	        steps {
			bat 'mvn test'
	       
        }
                    
   	}	
        

	stage('SonarQube'){
         steps{
            bat script: '''mvn sonar:sonar \
		 -Dsonar.host.url=http://localhost:9000 \
 		-Dsonar.login=c3c77358a6c58eaf9603b597f2010d02b89094a5'''
          }
	}
	
	
	
	stage("Nexus") {
            steps {
                script{
				
				def mavenPom = readMavenPom file:'pom.xml'
				//def
				nexusArtifactUploader artifacts:[
					[
						artifactId:'Sample-Mobile-Application',
						classifier:'',
						file:"target/Sample-Mobile-Application-${mavenPom.version}.jar",
						type:'jar'
					]
				],
				credentialsId:NEXUS_CREDENTIAL_ID,
				groupId:'com.cg.sma',
				nexusUrl:NEXUS_URL,
				nexusVersion:NEXUS_VERSION,
				protocol:'http',
				repository:NEXUS_REPOSITORY,
				version:"${mavenPom.version}"
				}
            }
    }

	
}
post{
                         junit '/target/test-reports/*.xml'
                 }
}
