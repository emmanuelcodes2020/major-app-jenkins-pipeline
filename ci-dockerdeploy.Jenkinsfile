pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage( 'Docker Run') {
            steps {
              sh """
               docker run -d -p 81:81 --name super-container3  416591745024.dkr.ecr.eu-west-2.amazonaws.com/docker-repo/super-app

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
