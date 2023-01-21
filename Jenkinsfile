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
                script {
                    sh "echo '//registry.npmjs.org/:_authToken=\${NPM_TOKEN}' >> .npmrc"
                    withEnv(["NPM_TOKEN=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"]) {
                        sh "cat .npmrc"
                        sh "npm whoami"
                        sh "npm version minor --no-git-tag-version"
                        sh "npm publish"
                    }
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