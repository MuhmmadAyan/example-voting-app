pipeline {
    agent any
    environment {
        SONARSERVER = 'sserver'
        SONARSCANNER = 'sonar'
    }

    stages {
        stage('TESTING SONAR_ANALYSIS') {
            steps {
                script {
                    def scannerHome = tool "${SONARSCANNER}"

                    withEnv(["PATH+SONAR=${scannerHome}/bin"]) {
                        sh '''sonar-scanner \
                               -Dsonar.projectKey=project \
                               -Dsonar.sources=. \
                               -Dsonar.host.url=http://13.235.244.108:9000 \
                               -Dsonar.login=sqp_58d710c5df0d32aa143ad1933292b3670c25b2ad '''
                        
                    }
                }
            }
        }

        stage('QG checking') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                    
                }
            }
        }
    }
}
