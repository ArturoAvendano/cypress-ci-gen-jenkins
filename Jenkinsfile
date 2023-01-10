
pipeline {
    agent any

    tools {nodejs "NodeJS19"}
    environment {
        CYPRESS_USERNAME     = credentials('lambdatest-username')
        CYPRESS_ACCESS_KEY = credentials('lambdatest-access-key')
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
                script{
                    jsonfile = readJSON file: 'cypress.env.json'
                    
                    jsonfile['username'] = echo ${CYPRESS_USERNAME}
                    jsonfile['access_key'] = echo ${CYPRESS_ACCESS_KEY}
                    writeJSON file: 'cypress.env.json', json: jsonfile
                      }
                echo "User is ${CYPRESS_USERNAME}"
                echo "Access key is ${CYPRESS_ACCESS_KEY}"
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

