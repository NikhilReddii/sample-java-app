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
        
}

}
