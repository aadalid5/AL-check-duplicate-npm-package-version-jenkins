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
                echo "publish"
            }
        }

        stage('post'){
            steps {
                sh "postmessage"
            }
        }
    }
}