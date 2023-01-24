pipeline {
    agent any
    
    tools { nodejs "node" }

    stages {
        stage('set remote'){
            steps{
                sshagent(["github-key-a-id"]){
                    script {
                        sh 'git remote set-url origin git@github.com:aadalid5/aa2-package.git'
                    }
                }
            }
        }

        stage ('install') {
            steps {
                sh 'node -v'
            }
        }

        stage('publish') {
            steps {
                withCredentials([gitUsernamePassword(credentialsId: 'git-hbrjenkins')]) {
                    sh "git fetch"
                    sh "git checkout main"
                    sh "git pull"
                    sh "git reset --hard HEAD"
                    
                }

                script {
                        sh "npm whoami"

                        newVersion = generateReleaseVersion("pr")
                        sh "npm pkg set version=${newVersion}"

                        if (!isVersionDuplicated()){
                            try{
                                sh "npm publish"
                            }catch(error){
                                sh "echo 'Deploy aborted with exception' ${error}"
                            }
                        } else {
                            sh "echo 'Reason: Version ${newVersion} already exists '"
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

def generateReleaseVersion(type) {
    def currentVersion = sh(script: "npm pkg get version | sed 's/\"//g'" , returnStdout: true)
    def newVersion = "${currentVersion.trim()}-${type}.${getShortHash()}"
    return newVersion
}

def getShortHash() {
    sh "git rev-parse --short HEAD > .git/shortID"
    def shortID = readFile(".git/shortID").trim()
    sh "rm .git/shortID"
    shortID
}

def isVersionDuplicated(){
    current = sh(script: "node -p -e \"require('./package.json').version\"" , returnStdout: true) // 0.0.17
    remote =  sh(script: "npm view . version", returnStdout: true) // 0.0.17-pr.xyz

    return current == remote
}