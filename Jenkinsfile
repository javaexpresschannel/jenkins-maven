pipeline {
    agent any 
    stages {
        stage('Compile & Clean') { 
            steps {

              
                    sh 'mvn clean compile'
                
                
            }
        }
        stage('Test') { 
            steps {
                 
                    sh 'mvn test'
                
            }
        }
        stage('Deploy') { 
            steps {
                
                    sh 'mvn package'
                    
                
            }
            
         
                
 
        }
        
         stage('archving') { 
           
            
            steps {
                       archiveArtifacts '/var/lib/jenkins/workspace/ProductionPipeline/target/*.jar'
            }
                
 
        }
    }
}
