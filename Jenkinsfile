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
                sh "npm set registry 'https://registry.npmjs.org'"
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