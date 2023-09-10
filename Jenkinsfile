pipeline {
    
	agent any

    stages{
        
        stage('TESTING SONAR_ANALYSIS'){
            steps {
                
            withSonarQubeEnv('sonar-server') {'''-Dsonar.projectKey=vote \
                     -Dsonar.sources=. \
                     -Dsonar.host.url=http://13.232.92.206:9000 \
                      -Dsonar.token=sqp_181c2ba1b448c17aadd3f54d9cfd03b300e585ea'''

            }
            
            }
        }
    }
}