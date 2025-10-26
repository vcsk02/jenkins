pipeline {
  agent any
  options { timestamps(); ansiColor('xterm') }
  triggers { githubPush() }   // pairs with your /github-webhook/ endpoint

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build') {
      steps {
        sh '''
          echo "🔧 Build step (replace me with your real build)"
          # e.g., mvn -B -DskipTests package
          # e.g., npm ci && npm run build
          # e.g., python -m build
        '''
      }
    }

    stage('Test') {
      steps {
        sh '''
          echo "🧪 Test step (replace me with your real tests)"
          # e.g., mvn -B test
          # e.g., npm test -- --ci --reporters=jest-junit
          # e.g., pytest --junitxml=reports/junit.xml

          # Make a tiny JUnit report so Jenkins always shows test results
          mkdir -p reports
          cat > reports/sample-test.xml <<'EOF'
          <testsuite tests="1" failures="0" name="smoke">
            <testcase classname="smoke" name="always passes" time="0.001"/>
          </testsuite>
          EOF
        '''
      }
    }
  }

  post {
    always {
      junit allowEmptyResults: true, testResults: 'reports/**/*.xml'
      archiveArtifacts artifacts: 'reports/**', onlyIfSuccessful: true, fingerprint: true
    }
  }
}
