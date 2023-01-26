pipeline {
    agent any
    
    tools { nodejs "node" }

    stages {
        stage ('install') {
            steps {
                sh 'node -v'
            }
        }

        stage('publish') {
            steps {
                script {
                        sh "npm whoami"

                        newVersion = generateReleaseVersion("pr")
                        sh "npm pkg set version=${newVersion}"

                        if (!isVersionDuplicated()){
                            try{
                                sh "npm publish"
                            }catch(error){
                                sh "echo 'DEPLOY ABORTED WITH ERROR' ${error}"
                            }
                        } else {
                            sh "echo '**PUBLISHIN SKIPPED** REASON: Version ${newVersion} already exists '"
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
    def current = sh(script: "node -p -e \"require('./package.json').version\"" , returnStdout: true)
    try{ 
        sh "npm view aa2-package@${current}" 
        return true // is duplicated
    } catch(error){
        // is not duplicated
        return false
    }
}