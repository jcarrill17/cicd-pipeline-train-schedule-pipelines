pipeline {
  agent any
  environment {
    SPECTRAL_DSN = credentials('spectral-dsn')
  }
  stages {
    stage('install Spectral') {
      steps {
        sh "curl -L "https://get.spectralops.io/latest/x/sh?dsn=$SPECTRAL_DSN" | sh" 
      }
    }
    stage('scan for issues') {
      steps {
        sh "$HOME/.spectral/spectral scan"
      }
    }
    stage ('Build') {
      steps {
        echo 'Running build automation'
        sh './gradlew build --no-daemon'
        archiveArtifacts artifacts: 'dist/trainSchedule.zip'
      }
    }
  }  
}
