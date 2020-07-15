pipeline {
    agent any 

    triggers {
        pollSCM('* * * * *')
    }

    stages {

        stage('Wipeout workspace') {

            steps {
                deleteDir()
                checkout scm
            }

        }

        
        stage('Compile & Clean') { 
            steps {

                    sh 'printenv'
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
                archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
