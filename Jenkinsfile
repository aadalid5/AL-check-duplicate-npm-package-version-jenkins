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
                sh "npm config set registry http://registry.npmjs.org"
                sh "npm cache clean -f"
                sh "npm start"
                sh "npm run dopublish"
            }
        }

        stage('post'){
            steps {
                sh "echo 'postmessage'"
            }
        }
    }
}