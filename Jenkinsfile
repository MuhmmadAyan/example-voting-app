pipeline {
    agent any
    environment {
        SONARSERVER = 'sserver'
        SONARSCANNER = 'sonar'
        registryv = "mohammadayan/vote"
        registryw = "mohammadayan/worker"
        registryr = "mohammadayan/result"
        registrys = "mohammadayan/seeddata"
        registryCredential = 'dockerhub'
    }
    stages {
        stage('Initial Setup') {
            steps {
                script {
                    scannerHome = tool "${SONARSCANNER}"
                }
            }
        }
        stage('Sonar Analysis and Quality Gates') {
            steps {
                script {
                    withSonarQubeEnv("${SONARSERVER}") {
                        sh """
                            "${scannerHome}"/bin/sonar-scanner \
                            -Dsonar.projectKey=Voting-App \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://13.233.111.148:9000 \
                            -Dsonar.token=sqp_96442758c0a6472f6faf110ddb7a210abc9b406d
                        """
                        
                    }
                    timeout(time: 10, unit: 'MINUTES') {
               waitForQualityGate abortPipeline: true
                }
            }
        }
    }
        stage('Building Docker Images'){
            steps{
            script{
                    dockerImage1 = docker.build registryv + ":$BUILD_NUMBER", "./vote"
                    dockerImage2 = docker.build registryw + ":$BUILD_NUMBER", "./worker"
                    dockerImage3 = docker.build registryr + ":$BUILD_NUMBER", "./result"
                    dockerImage4 = docker.build registrys + ":$BUILD_NUMBER", "./seed-data"


                }
            }
        }
        stage('Pushing Images to DockerHub'){

        steps{
            script{
                docker.withRegistry( '', registryCredential ) {
                dockerImage1.push("$BUILD_NUMBER")
                dockerImage1.push('latest')
                }
                docker.withRegistry( '', registryCredential ) {
                dockerImage2.push("$BUILD_NUMBER")
                dockerImage2.push('latest')
                }
                docker.withRegistry( '', registryCredential ) {
                dockerImage3.push("$BUILD_NUMBER")
                dockerImage3.push('latest')
                }
                docker.withRegistry( '', registryCredential ) {
                dockerImage4.push("$BUILD_NUMBER")
                dockerImage4.push('latest')
                }
            }
        }
}
        stage('Removing Build DockerImages From Jenkins'){
            steps{
                script{
                    sh 'docker rmi -f $(docker images -q)'
                    
                }
            }
        }
        stage('Deploying Images on EKS cluster'){
            steps{
                script{
                 
                sh 'kubectl create -f k8s-specifications/'

                }
            }
        }
        
}
}