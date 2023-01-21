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
                withCredentials([gitUsernamePassword(credentialsId: 'git-hbrjenkins')]) {
                    sh "git pull"
                }

                script {
                        sh "cat .npmrc"
                        sh "npm whoami"
                        sh "npm version minor"
                        sh "npm publish"
                }

                withCredentials([gitUsernamePassword(credentialsId: 'git-hbrjenkins')]) { 
                    script {
                        sh "git push --no-verify"
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