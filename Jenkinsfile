pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
     options {
                timeout(time: 1, unit: 'HOURS')
                disableConcurrentBuilds() 
            }
    //  environment { 
    //     packageVersion = ''
    //     nexusURL = '172.31.13.69:8081'
    //  }
     parameters {
        string(name: 'version', defaultValue: '1.0.0', description: 'What is the version?')
     }
     stages { 
        stage('deploy') {
            steps {
                echo '
            }
        }
    }