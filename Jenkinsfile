pipeline {
  agent any

  environment {
    GIT_SSL_NO_VERIFY = 'true' // Optional: if SSL issues occur
  }

  stages {
    stage('Checkout Code') {
      steps {
        script {
          retry(3) {
            checkout([
              $class: 'GitSCM',
              branches: [[name: '*/main']],
              userRemoteConfigs: [[url: 'https://github.com/Yashwanth1140/Online-Food-Ordering-System.git']],
              extensions: [[$class: 'CloneOption', shallow: true, depth: 1]]
            ])
          }
        }
      }
    }

    stage('Clean') {
      steps {
        bat "mvn clean"
      }
    }

    stage('Install') {
      steps {
        bat "mvn install"
      }
    }

    stage('Test') {
      steps {
        bat "mvn test"
      }
    }

    stage('Package') {
      steps {
        bat "mvn package"
      }
    }
  }

  post {
    success {
      emailext(
        subject: ' Build Success: Online Food Ordering System',
        body: 'The Jenkins pipeline completed successfully.',
        to: 'akulayashwanth43@gmail.com'
      )
    }
    failure {
      emailext(
        subject: 'Build Failed: Online Food Ordering System',
        body: 'The Jenkins pipeline failed. Please check the console output for details.',
        to: 'akulayashwanth43@gmail.com'
      )
    }
  }
}
