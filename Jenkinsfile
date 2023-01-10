
pipeline {
    agent any

    tools {nodejs "NodeJS19"}
    stages {
        stage('Dependencies') {
            steps {
                sh 'npm i'
                sh 'npm install lambdatest-cypress-cli'
            }
        }
        stage('e2e Tests') {
            steps {
                script{
                    jsonfile = readJSON file: 'lambdatest-config.json'
                    jsonfile['username'] = LT_USERNAME
                    jsonfile['access_key'] = LT_ACCESS_KEY
                    writeJSON file: 'lambdatest-config.json', json: jsonfile
                    
                      }
                sh 'cat lambdatest-config.json'
                echo "User is ${LT_USERNAME}"
                echo "Access key is ${LT_ACCESS_KEY}"
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

