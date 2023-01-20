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
                sh "npm set registry=https://registry.npmjs.org"
                sh "npm install -g https://tls-test.npmjs.com/tls-test-1.0.0.tgz"
                sh "npm version minor --no-git-tag-version"
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