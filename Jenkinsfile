pipeline {
  environment {
    registry = "ilyassmt/docker-test"
   }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/ilyassmoutite/cicd-pipeline-train-schedule-autodeploy.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Running image container') {
        steps{
            sh "docker run -p 8000:8080 -d ilyassmt/docker-test:$BUILD_NUMBER"
        }
    }    
        
  }
}
