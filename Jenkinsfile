pipeline {
    agent any 
    stages {
        stage('Compile & Clean') { 
            steps {

                maven(maven: 'maven_3.6.3'){
                    sh 'mvn clean compile'
                }
                
            }
        }
        stage('Test') { 
            steps {
                 maven(maven: 'maven_3.6.3'){
                    sh 'mvn test'
                } 
            }
        }
        stage('Deploy') { 
            steps {
                 maven(maven: 'maven_3.6.3'){
                    sh 'mvn package'
                } 
            }
        }
    }
}
