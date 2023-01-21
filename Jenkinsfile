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
                    sh "cat .npmrc"
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