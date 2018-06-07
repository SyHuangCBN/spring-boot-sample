pipeline {
  agent any
  stages {
    stage('checkout project') {
      steps {
        checkout scm
        sh 'mvn cobertura:cobertura test'
      }
    }
    stage('TEST') {
      steps {
        sh 'mvn cobertura:cobertura test'
      }
    }
    stage('Report') {
      parallel {
        stage('Report') {
          steps {
            junit 'target/surefire-reports/*.xml'
          }
        }
        stage('Report2') {
          steps {
            cobertura(coberturaReportFile: 'target/site/cobertura/coverage.xml')
          }
        }
      }
    }
  }
  post {
    always {
      echo 'I will always say Hello again!'

    }

    success {
      echo 'success!'

    }

    failure {
      echo 'failure!'

    }

  }
}