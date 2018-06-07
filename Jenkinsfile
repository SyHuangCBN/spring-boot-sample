pipeline {
  agent any
  stages {
    stage('checkout project') {
      steps {
        checkout scm
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
    stage('Package') {
      steps {
        sh 'mvn package'
      }
    }
    stage('Artiche') {
      steps {
        archiveArtifacts 'target/*.jar'
      }
    }
    stage('wait for confirm') {
        input {
            message "Should we deploy?"
            ok "Yes, we should."
            submitter "admin"
            parameters {
                string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
            }
        }
        steps {
            echo "Hello, ${PERSON}, nice to meet you."
        }
    }
    stage('Deploy') {
      steps {
        sh 'make deploy-default'
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