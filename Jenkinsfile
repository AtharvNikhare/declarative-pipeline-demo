// Use nested stages so we can run preparation steps and then run parallel test stages
stage('Test') {
  stages {
    stage('Prepare') {
      steps {
        sh 'chmod a+x run_build_script.sh'
        sh './run_build_script.sh'
      }
    }

    stage('Parallel Tests') {
      parallel {
        stage('Test On Windows') {
          steps {
            echo "Running tests on Windows"
          }
        }
        stage('Test On Linux') {
          steps {
            echo "Running tests on Linux"
          }
        }
        stage('Confirm Deploy to staging') {
          steps {
            timeout(time: 60, unit: 'SECONDS') {
              input(message: "Okay to Deploy?", ok: "Let's Do it!")
            }
          }
        }
        stage('Deploy to Staging') {
          steps {
            echo "Deploying to staging..."
          }
        }
        stage('Confirm Deploy to production') {
          steps {
            timeout(time: 60, unit: 'SECONDS') {
              input(message: "Okay to Deploy?", ok: "Let's Do it!")
            }
          }
        }
        stage('Deploy to Production') {
          steps {
            echo "Deploying to production..."
          }
        }
      }
    }
  }
}
