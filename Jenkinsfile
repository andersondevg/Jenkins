pipeline {
    agent none

    stages {
        stage('build') {
            agent{
                docker{
                    image 'node'
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
    }
}