
pipeline {
    agent any

    tools {nodejs "NodeJS19"}
    environment {
        LT_USERNAME     = credentials('lambdatest-username')
        LT_ACCESS_KET = credentials('lambdatest-access-key')
    stages {
        stage('Dependencies') {
            steps {
                sh 'npm i'
                sh 'npm install lambdatest-cypress-cli'
            }
        }
        stage('e2e Tests') {
            steps {
                sh 'npm run cypress:lambda'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}

