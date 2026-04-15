
pipeline {
    agent {
        label 'dev'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')          // Timeout counter starts AFTER agent is allocated
        disableConcurrentBuilds()        // to queue a build when there’s already an executing build of the Pipeline
        ansiColor('xterm')
    }
    environment{
        def appVersion = '' //variable declaration
    }
    stages {
        stage('read the version'){
            steps{
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo 'application version: $appVersion'
                }
            }
        }
        stage ('Install dependencies') {
            steps {
                sh '''
                npm install
                ls -lrt
                echo 'application version: $appVersion'
                ''' 
            }
        }
        stage('Build'){
            steps{
                sh '''
                zip -q -r backend-${appVersion}.zip * -x Jenkinsfile -x backend-${appVersion}.zip
                ls -ltr
                '''
            }
        }
    
        
    }
    
    post { 
        always { 
            echo 'I will always say Hello again!'
            //deleteDir()    // to delete workspace after the build
        }
        success { 
            echo 'I will run when pipeline is success'
        }
        failure { 
            echo 'I will run when pipeline is failure'
        }
    }
}