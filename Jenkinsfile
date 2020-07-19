pipeline {
    agent any 
    stages {
        stage('Compile and Clean') { 
            steps {

                sh "mvn clean compile"
            }
        }
        stage('Test') { 
            steps {
                sh "mvn test site"
            }
            
             post {
                always {
                    junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'   
                }
            }     
        }

        stage('Build Docker image'){
            steps {
                sh 'docker build -t anvbhaskar/my-app:${BUILD_NUMBER}'
            }
        }

        stage('Docker Login & Push'){
            
            steps {
                withCredentials([string(credentialsId: 'dockerPWD', variable: 'dockerPwd')]) {
               sh 'docker login -u anvbhaskar -p ${dockerPwd}'
            }                
        }

        stage('Deploy') { 
            steps {
                sh "mvn package"
            }
        }

        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
