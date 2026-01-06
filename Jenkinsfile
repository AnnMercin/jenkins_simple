pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate') {
            steps {
                sh '''
                  echo "Validating application..."
                  test -f app.sh
                '''
            }
        }

        stage('Run Script') {
            steps {
                sh '''
                  chmod +x app.sh
                  ./app.sh
                '''
            }
        }

        stage('Promote Development → Prod') {
            when {
                branch 'development'
            }
            steps {
                sh '''
                  echo "Promoting development to main..."

                  git config user.name "jenkins"
                  git config user.email "jenkins@ci.local"

                  git fetch origin
                  git checkout main
                  git merge development --no-ff
                  git push origin main
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline passed 🎉"
        }
        failure {
            echo "Pipeline failed ❌ — prod not touched"
        }
    }
}

