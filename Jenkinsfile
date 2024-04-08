pipeline {
    agent any

    parameters{
        booleanParam(name: 'PLAN', defaultValue: false, description: 'enable to plan infrastructure')
        booleanParam(name: 'APPLY', defaultValue: false, description: 'enable to apply infrastructure')
        booleanParam(name: 'DESTROY', defaultValue: false, description: 'enable to destroy infrastructure')
        booleanParam(name: 'DEPLOY', defaultValue: false, description: 'enable to deploy infrastructure')
    }

    stages {
        stage('Clone git repository') {
            steps {
               sh "git clone git@github.com:emmanuelcodes2020/git-terraform-demo.git"
               sh 'pwd'
            }
        }
        
        stage('Configure Terraform backend') {
            steps {

               sh """
                cd git-terraform-demo
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
                cd git-terraform-demo
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
                cd git-terraform-demo
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
                cd git-terraform-demo
                terraform destroy --auto-approve
                """

            }
        }

        stage('Deploy') {
            when{
                expression{params.DEPLOY == true}
            }
            steps {
               sh """
                git clone git@github.com:emmanuelcodes2020/ansible-playbook-major.git
                cd ansible-playbook-major
                ansible webserver -m ping -i aws_ec2.yml -u ec2-user --private-key=~/.ssh/londonserver.pem
                ansible-galaxy install -r requirements.yml --roles-path roles
                ansible-playbook -i aws_ec2.yml site.yml -b -u ec2-user --private-key=~/.ssh/londonserver.pem
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
