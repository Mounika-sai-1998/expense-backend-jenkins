
pipeline {
    agent {
        label 'dev'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')          // Timeout counter starts AFTER agent is allocated
        disableConcurrentBuilds()        // to queue a build when there’s already an executing build of the Pipeline
        ansiColor('xterm')
    }
     
    stages {
        stage ('testing') {
            steps {
                sh 'echo this is testing' 
            }
        }
    
        
    }
    
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()    // to delete workspace after the build
        }
        success { 
            echo 'I will run when pipeline is success'
        }
        failure { 
            echo 'I will run when pipeline is failure'
        }
    }
}