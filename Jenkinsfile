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
                    sh "echo token: $NPM_TOKEN"
                    sh "echo '//registry.npmjs.org/:_authToken=\${NPM_TOKEN}' >> .npmrc"
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