pipeline {
    agent any
    environment {
        SONARSERVER = 'sserver'
        SONARSCANNER = 'sonar'
    }

    stages {
        stage('TESTING SONAR_ANALYSIS') {
            steps {
                withSonarQubeEnv("${SONARSERVER}") {
                    sh """
                        "${SONARSCANNER}"/bin/sonar-scanner \
                        -Dsonar.projectKey=klll \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://13.235.244.108:9000 \
                        -Dsonar.token=sqp_f6b3f16f6ae55b0c3284457946dbd38601439867
                         
                    """
                }
            }
        }
    }
}
