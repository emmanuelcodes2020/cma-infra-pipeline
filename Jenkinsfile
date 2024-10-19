pipeline {
    agent {label 'node-1'}

    parameters{
        booleanParam(name: 'PLAN', defaultValue: false, description: 'enable to plan infrastructure')
        booleanParam(name: 'APPLY', defaultValue: false, description: 'enable to apply infrastructure')
        booleanParam(name: 'DESTROY', defaultValue: false, description: 'enable to destroy infrastructure')
    }

    stages {
        stage('Clone git repository') {
            steps {
               sh "git clone git@github.com:emmanuelcodes2020/terraform-cma-application.git"
               sh 'pwd'
            }
        }
        
        stage('Configure Terraform backend') {
            steps {

               sh """
                cd terraform-cma-application
                terraform init
                """
            }
        }

        stage('Terraform Plan') {
            when{
                expression{params.PLAN == true}
            }
            steps {
                sh """
                cd terraform-cma-application
                terraform plan
                """
              
            }
        }
        
        stage('Terraform apply') {
            when{
                expression{params.APPLY == true}
            }
            steps {

               sh """
                cd terraform-cma-application
                terraform apply --auto-approve
                """
            }
        }
        
        stage('Terraform destroy') {
            when{
                expression{params.DESTROY == true}
            }
            steps {
               sh """
                cd terraform-cma-application
                terraform destroy --auto-approve
                """

            }
        }

   }
   post{
        cleanup{
            cleanWs()
        }
   }

        
}
