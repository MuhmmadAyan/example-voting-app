pipeline {
    
	agent any

    stages{
        
        stage('TESTING SONAR_ANALYSIS'){
            steps {
            environment {
             scannerHome = tool 'sonar'
          }
           
               withSonarQubeEnv('sserver') {
             sh '''${scannerHome}/bin/sonar-scanner \
             -Dsonar.projectKey=project \
             -Dsonar.sources=. \
             -Dsonar.host.url=http://13.235.244.108:9000 '''
             

            }
            
            }
        }
    }
}