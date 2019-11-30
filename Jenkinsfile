pipeline {
    agent any
    environment {
        //be sure to replace "willbla" with your own Docker Hub username
        DOCKER_IMAGE_NAME = "ilyassmt/hello"
    }
    stages {
     
      
 
        stage('DeployToProduction') {
         
            steps {
                input 'Deploy to Production?'
                milestone(1)
                withCredentials([usernamePassword(credentialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    script {
                        sh "  ssh   $USERNAME@$prod_ip \"docker pull ilyassmt/hello\""
                        try {
                            sh "  ssh   $USERNAME@$prod_ip \"docker stop ilyassmt/hello\""
                            sh "   ssh   $USERNAME@$prod_ip \"docker rmi -f ilyassmt/hello\""
                        } catch (err) {
                            echo: 'caught error: $err'
                        }
                        sh " ssh  $USERNAME@$prod_ip \"docker run --restart always --name ilyassmt/hello -d ilyassmt/hello\""
                    }
                }
            }
        }
    }
}
