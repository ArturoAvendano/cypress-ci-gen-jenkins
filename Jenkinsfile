
pipeline {
    agent any

    tools {nodejs "NodeJS19"}
    environment {
        LT_USERNAME     = credentials('lambdatest-username')
        LT_ACCESS_KEY = credentials('lambdatest-access-key')
    }
    stages {
        stage('Dependencies') {
            steps {
                sh 'npm i'
                sh 'npm install lambdatest-cypress-cli'
            }
        }
        stage('e2e Tests') {
            steps {
                echo "User is ${LT_USERNAME}"
                echo "Access key is ${LT_ACCESS_KEY}"
                sh 'npm run cypress:lambda --env username=${LT_USERNAME},access_key=${LT_ACCESS_KEY}'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}

