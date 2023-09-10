pipeline {
    
	agent any

    stages{
        
        stage('TESTING SONAR_ANALYSIS'){
            steps {
            environment {
            scannerHome = tool 'sonar-server'
          }
           
               withSonarQubeEnv('sonar-server') {
               sh '''${scannerHome}/bin/sonar-scanner sonar-scanner \
            -Dsonar.projectKey=project \
            -Dsonar.sources=. \
            -Dsonar.host.url=http://13.235.244.108:9000 \
            -Dsonar.token=sqp_694a2edcfa170fc0cd1555c13e8faf559fe7f76f'''

            }
            
            }
        }
    }
}