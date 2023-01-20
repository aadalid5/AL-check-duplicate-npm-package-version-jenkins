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
                sh "//registry.npmjs.org/:_authToken=\"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\" >> .npmrc"
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