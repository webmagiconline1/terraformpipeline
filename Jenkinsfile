pipeline{
    agent any
    
    parameters {
        choice choices: ['plan', 'apply', 'destroy'], name: 'action'
    }
    
    stages{
        stage("init"){
            steps{
                sh "terraform init"
            }
        }
        stage("plan"){
            when{
                expression { params.action == 'plan' }
            }
            steps{
                sh "terraform workspace select dev"
                sh "terraform plan"
            }
        }
        stage("apply"){
            when{
                expression { params.action == 'apply' }
            }
            steps{
                sh "terraform workspace select dev"
                sh "terraform apply -var-file=prod.tfvars -auto-approve"
            }
        }
        stage("destroy"){
            when{
                expression { params.action == 'destroy' }
            }
            steps{
                sh "terraform workspace select dev"
                sh "terraform destroy -var-file=prod.tfvars -auto-approve"
            }
        }
    }
}
