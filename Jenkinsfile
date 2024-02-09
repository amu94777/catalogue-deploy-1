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
        string(name: 'environment', defaultValue: "dev", description: 'What is the environment?')
     }
     stages { 
        stage('print the version') {
            steps {
                echo "the version is : ${params.version}"
                echo "the environment is : ${params.environment}"
            }
        }
    }

post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        failure { 
            echo 'this runs when pipeline is failed, used generally to send some alerts'
        }
        success{
            echo 'I will say Hello when pipeline is success'
        }
    }
}


