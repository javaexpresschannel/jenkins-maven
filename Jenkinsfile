pipeline {
    agent any 
    stages {
        stage('Compile and Clean') { 
            steps {

                bat "mvn clean compile"
            }
        }
        stage('Test') { 
            steps {
                bat "mvn test site"
            }
            
             post {
                always {
                    junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'   
                }
            }     
        }

        stage('deploy') { 
            steps {
                bat "mvn package"
            }
        }


        stage('Build Docker image'){
            steps {
                bat 'docker build -t anvbhaskar/docker_jenkins_pipeline:${BUILD_NUMBER} .'
            }
        }

        stage('Docker Login'){
            
            steps {
                 withCredentials([string(credentialsId: 'DockerId', variable: 'Dockerpwd')]) {
                    bat "docker login -u anvbhaskar -p ${Dockerpwd}"
                }
            }                
        }

        stage('Docker Push'){
            steps {
                bat 'docker push anvbhaskar/docker_jenkins_pipeline:${BUILD_NUMBER}'
            }
        }
        
        stage('Docker deploy'){
            steps {
                bat 'docker run -itd -p 8081:8080 anvbhaskar/springboot:0.0.3'
            }
        }

        
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
