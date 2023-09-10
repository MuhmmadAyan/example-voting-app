pipeline {
    agent any
    environment {
        SONARSERVER = 'sserver'
        SONARSCANNER = 'sonar'
        registryv = "mohamadayan/vote"
        registryw = "mohammadayan/worker"
        registryr = "mohammadayan/result"
        registrys = "mohammadayan/seeddata"
        registryCredential = 'dockerhub'
    }
    stages {
        stage('Setup') {
            steps {
                script {
                    scannerHome = tool "${SONARSCANNER}"
                }
            }
        }
        stage('TESTING SONAR_ANALYSIS') {
            steps {
                script {
                    withSonarQubeEnv("${SONARSERVER}") {
                        sh """
                            "${scannerHome}"/bin/sonar-scanner \
                            -Dsonar.projectKey=klll \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://13.235.244.108:9000 \
                            -Dsonar.token=sqp_f6b3f16f6ae55b0c3284457946dbd38601439867
                        """
                        
                    }
                    timeout(time: 10, unit: 'MINUTES') {
               waitForQualityGate abortPipeline: true
                }
            }
        }
    }
        stage('building docker images'){
            steps{
            script{
                    dockerImage1 = docker.build registryv + ":$BUILD_NUMBER", "./vote"
                    dockerImage2 = docker.build registryw + ":$BUILD_NUMBER", "./worker"
                    dockerImage3 = docker.build registryr + ":$BUILD_NUMBER", "./result"
                    dockerImage4 = docker.build registrys + ":$BUILD_NUMBER", "./seed-data"


                }
            }
        }
        stage{

        
        steps{
            script{
                docker.withRegistryv( '', registryCredential ) {
                dockerImage1.push("$BUILD_NUMBER")
                dockerImag1e1.push('latest')
                }
                docker.withRegistryw( '', registryCredential ) {
                dockerImage2.push("$BUILD_NUMBER")
                dockerImag2.push('latest')
                }
                docker.withRegistryr( '', registryCredential ) {
                dockerImage3.push("$BUILD_NUMBER")
                dockerImage3.push('latest')
                }
                docker.withRegistrys( '', registryCredential ) {
                dockerImage4.push("$BUILD_NUMBER")
                dockerImage14.push('latest')
                }
            }
        }
}
}
}