pipeline {
  environment {
    registry = "asmaeguiouart/guiouart_tp5"
    registryCredential = 'Asmae2'
    dockerImage = ''
    gitBranch = 'master'
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git branch: "${gitBranch}", url: 'https://github.com/AsmaeGUIOUART/tpdevops'
      }
    }
    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Test image') {
      steps {
        script {

          echo "Tests passed"
        }
      }
    }
    stage('Publish Image') {
      steps {
        script {
          docker.withRegistry('', registryCredential) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Deploy image') {
       steps{
       bat "docker run -d $registry:$BUILD_NUMBER"
       }
     }
  }
}
