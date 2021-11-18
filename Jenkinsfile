pipeline{
agent any
stages{
        stage('build'){

               steps{
                      bat 'mvn compile'
                    }
}
        stage('unit testing'){
               steps{
                      bat 'mvn test'
                    }
}
        stage('SonarQube'){
         steps{
            bat script: '''mvn sonar:sonar \
		 -Dsonar.host.url=http://localhost:9000 \
 		-Dsonar.login=[c3c77358a6c58eaf9603b597f2010d02b89094a5'''
              }
}
        
}

}
