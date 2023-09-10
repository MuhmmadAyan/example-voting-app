pipeline {
    agent any
    environment {
        SONARSERVER = 'sserver'
        SONARSCANNER = 'sonar'
    }

    stages {
        stage('TESTING SONAR_ANALYSIS') {
            steps {
                environment {
                    scannerHome = tool "${SONARSCANNER}"
                }

                withSonarQubeEnv("${SONARSERVER}") {
                    sh '''${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=project \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://13.235.244.108:9000
                    '''
                }
            }
        }
    }
}
