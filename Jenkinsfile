pipeline {
  environment {
    registry = "ilyassmt/docker-test"
    registryCredential = "DockerHub"
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
          image=docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Running image container') {
        steps{
            sh "docker run -p 8000:8080 -d $registry:$BUILD_NUMBER"
        }
    }    
    
    stage('Deploy Image') {
       steps{    
         script {
           docker.withRegistry( '', registryCredential ) { image.push() }
         }
       }
    }
        
  }
}
