pipeline {
    agent any
    environment {
        //be sure to replace "willbla" with your own Docker Hub username
        DOCKER_IMAGE_NAME = "ilyassmt/hello"
    }
    stages {
     
      
 
        stage('DeployToProduction') {
         
            steps {
                  withCredentials([usernamePassword(credentialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    script {
                         
                        sh "  ssh   ilyass@192.168.1.116 \"sudo docker pull ilyassmt/hello\""
                        try {
                            sh "  ssh  ilyass@192.168.1.116 \"sudo docker stop ilyassmt/hello\""
                            sh "   ssh   ilyass@192.168.1.116 \"sudo docker rmi -f ilyassmt/hello\""
                        } catch (err) {
                            echo: 'caught error: $err'
                        }
                        sh " ssh  ilyass@192.168.1.116 \"docker run  ilyassmt/hello \""
                    }
                }
            }
        }
    }
}
