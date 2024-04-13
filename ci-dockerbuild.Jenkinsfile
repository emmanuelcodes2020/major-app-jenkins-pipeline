pipeline {
    agent {label "super-agent"}

    stages {
        stage( 'Current Location') {
            steps {
             
              sh "pwd"
            }
        }
        stage( 'Docker versioning') {
            steps {
              sh """
              echo $USER
              sudo usermod -aG docker $USER
              sudo chmod 777 /var/run/docker.sock
              pwd
              docker version
              docker ps
              ls -lrt
              """
            }
        }
        stage( 'Git Clone and Change Directory') {
            steps {
              sh """
              git clone git@github.com:emmanuelcodes2020/docker-major-demo.git
              pwd
              cd docker-major-demo
              """
            }
        }
        stage( 'Docker build') {
            steps {
              sh """
               docker build -t super-app ./docker-major-demo
              """
            }
        }
        stage( 'Docker push') {
            steps {
              sh """
               docker push 416591745024.dkr.ecr.eu-west-2.amazonaws.com/docker-repo/super-app
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