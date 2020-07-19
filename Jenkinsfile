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

        stage('deploy') { 
            steps {
                sh "mvn package"
            }
        }


        stage('Build Docker image'){
            steps {
                sh 'docker build -t anvbhaskar/my-app:${BUILD_NUMBER} .'
            }
        }

        stage('Docker Login'){
            
            steps {
                withCredentials([string(credentialsId: 'dockerPWD', variable: 'dockerPwd')]) {
               sh 'docker login -u anvbhaskar -p ${dockerPwd}' }
            }                
        }

        stage('Docker Push'){
            steps {
                sh 'docker push anvbhaskar/my-app:${BUILD_NUMBER}'
            }
        }

        
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
