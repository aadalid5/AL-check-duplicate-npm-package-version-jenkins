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
                withEnv(['NPM_TOKEN=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']) {
                    sh echo 'name: $NPM_TOKEN'
                    sh "npm whoami"
                    sh "npm version minor --no-git-tag-version"
                    sh "npm publish"
                }
            }
        }

        stage('post'){
            steps {
                sh "echo 'postmessage'"
            }
        }
    }
}