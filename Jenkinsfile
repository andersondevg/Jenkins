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
        }        
    }
}