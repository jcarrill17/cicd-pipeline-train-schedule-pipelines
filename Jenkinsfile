pipeline {
  agent any
  environment {
    SPECTRAL_DSN = credentials('spectral-dsn')
  }
  stages {
    stage('install Spectral') {
      steps {
        sh 'curl -L "https://get.spectralops.io/latest/x/sh?dsn=https://spu-8656aeb0678849c3a10a8fe60a670813@spectral-us.checkpoint.com" | sh'
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
