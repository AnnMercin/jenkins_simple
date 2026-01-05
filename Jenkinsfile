pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AnnMercin/jenkins_simple.git'
            }
        }

        stage('Run Script') {
            steps {
                sh 'chmod +x app.sh'
                sh './app.sh'
            }
        }
    }
}

