pipeline {
  environment {
    imagename = "flask"
    registryCredential = 'DockerHubCredentials'
    dockerImage = ''
  }  
  agent any
    stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/surendrahari09/Github_Docker_Dhub_Ec2.git', branch: 'master', credentialsId: 'GithubCredentails'])

      }
    }
  stages {
    stage('Building image') {
      steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
  }
}
stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
        stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')
              
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"

      }
    }
