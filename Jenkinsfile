pipeline {
    agent none

    stages {
        stage('build') {
            agent{
                docker{
                    image 'andersondevg/nj8'
                }
            }
            steps {
                dir('website'){
                    sh 'npm i'
                    sh 'npm run build'
                }
            }
            post { 
                success { 
                    archiveArtifacts artifacts: "website/build/test-site/", fingerprint: true
                }
            }
        }
        stage('test'){
            parallel{
                stage('code analysis'){
                    agent{
                        docker{
                            image 'andersondeg/nj8'
                            args '--network readetrabalho_devopsjenkins'
                        }
                    }
                    environment{
                        scannerHome = tool 'sonarqube'
                    }
                }
                steps{
                    withSonarQubeEnv('sonarqube'){
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                    timeout(time: 10, unit: 'MINUTES'){
                        waitForQualityGate abortPipeline: true
                    }
                }
            }
        }        
    }
}