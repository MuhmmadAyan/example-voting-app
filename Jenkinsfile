pipeline {
    agent any
    environment {
        SONARSERVER = 'sserver'
        SONARSCANNER = 'sonar'
        ANALYSIS_ID = ''
    }

    stages {
        stage('TESTING SONAR_ANALYSIS') {
            steps {
                script {
                    def scannerHome = tool "${SONARSCANNER}"

                    withEnv(["PATH+SONAR=${scannerHome}/bin"]) {
                        script {
                            def scannerHome = tool "${SONARSCANNER}"

                            withEnv(["PATH+SONAR=${scannerHome}/bin"]) {
                                sh '''ANALYSIS_ID=$(sonar-scanner -Dsonar.projectKey=project -Dsonar.sources=. -Dsonar.host.url=http://13.235.244.108:9000 -Dsonar.login=sqp_58d710c5df0d32aa143ad1933292b3670c25b2ad | grep "ANALYSIS SUCCESSFUL, you can browse" | awk '{print $NF}'); \
                                      echo "ANALYSIS_ID=${ANALYSIS_ID}" >> env.properties'''
                            }
                        }
                    }
                }
            }
        }

        stage('QG checking') {
            steps {
                script {
                    def props = readProperties file: 'env.properties'
                    def analysisId = props['ANALYSIS_ID'].trim()
                    def qg = waitForQualityGate id: analysisId, abortPipeline: true
                    if (qg.status != 'OK') {
                        error "Pipeline aborted due to quality gate failure: ${qg.status}"
                    }
                }
            }
        }
    }
}
