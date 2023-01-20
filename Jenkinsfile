pipeline {
    agent any
    
    tools { nodejs "node" }

    stages {
        stage ('install') {
            steps {
                sh 'node -v'
                sh 'npm i'
            }
        }

        stage('publish') {
            steps {
                sh "npm version patch"
                sh "echo //registry.npmjs.org/:_authToken=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 >> .npmrc"
                sh "npm publish"
            }
        }

        stage('post'){
            steps {
                sh "echo 'postmessage'"
            }
        }
    }
}