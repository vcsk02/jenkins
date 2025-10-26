pipeline {
  agent any
  options { timestamps() }
  triggers { githubPush() }  
  stages {
    stage('Checkout') { steps { checkout scm } }

    stage('Build') {
      steps {
        sh '''
          echo "Build step goes here"
          # example: mvn -B -DskipTests package
          # example: npm ci && npm run build
        '''
      }
    }

    stage('Test') {
      steps {
        sh '''
          echo "Test step goes here"
          # example: mvn -B test
          # example: npm test -- --ci --reporters=junit --reporter-options "output=reports/junit.xml"
        '''
      }
    }
  }
  post {
    always {
      junit allowEmptyResults: true, testResults: 'reports/**/*.xml'
      archiveArtifacts artifacts: 'build/**', onlyIfSuccessful: true
    }
  }
}
