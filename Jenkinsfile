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
        string(name: 'version', defaultValue: '', description: 'What is the version?')
        string(name: 'environment', defaultValue: 'dev', description: 'What is the environment?')
        booleanParam(name: 'Destroy', defaultValue: 'false', description: 'What is Destroy?')
        booleanParam(name: 'Create', defaultValue: 'false', description: 'What is Create?')
     }
     stages { 
        stage('print the version') {
            steps {
                sh """
                echo "the version is : ${params.version}"
                echo "the environment is : ${params.environment}"
                """
            }
        }
        stage('Init') {
            steps {
                sh """
                   cd terraform
                   terraform init --backend-config=${params.environment}/backend.tf -reconfigure
                
                """
            }
        }
         stage('plan') {
             when{
                expression{
                    params.Create
                }
            }
            steps {
                sh """
                   cd terraform
                   terraform plan -var-file=${params.environment}/${params.environment}.tfvars -var="app_version=${params.version}"
                
                """
            }
        }
        stage('apply') {
             when{
                expression{
                    params.Create
                }
            }
            
            steps {
                sh """
                   cd terraform
                   terraform apply -var-file=${params.environment}/${params.environment}.tfvars -var="app_version=${params.version}" -auto-approve
                
                """
            }
        }
        stage('destroy') {
           when{
                expression{
                    params.Destroy
                }
            }


            steps {
                sh """
                   cd terraform
                   terraform destroy -var-file=${params.environment}/${params.environment}.tfvars -var="app_version=${params.version}" -auto-approve
                
                """
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


