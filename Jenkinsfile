pipeline {
  agent any
  stages {
    stage('Build ') {
      steps {
        sh 'docker build -t react-app .'
      }
    }

    stage('Deploy') {
      steps {
        sh 'docker run -itd --name react-container react-app'
      }
    }

  }
}