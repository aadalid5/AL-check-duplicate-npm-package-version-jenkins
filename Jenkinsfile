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
                sh 'echo "//registry.npmjs.org/:_authToken=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" >> ~/.npmrc'
                sh "publish"
            }
        }

        stage('post'){
            steps {
                sh "echo 'postmessage'"
            }
        }
    }
}