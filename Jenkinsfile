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
		steps{
			checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/NikhilReddii/sample-java-app.git']]])
		     }
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
						artifactId:'spring-boot-starter-parent',
						classifier:'',
						file:"target/sample-${mavenPom.version}.jar",
						type:'jar'
					]
				],
				credentialsId:NEXUS_CREDENTIAL_ID,
				groupId:'org.springframework.boot',
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
	always{
                         junit '/target/test-reports/*.xml'
                 }
              }
}
