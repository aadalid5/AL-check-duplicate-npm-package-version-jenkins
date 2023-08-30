pipeline {
    agent any
    
    tools { nodejs "node" }

    stages {
        stage ('install') {
            steps {
                script {
                    sh 'node -v'
                    echo "${env.test1}"
                    withCredentials([string(credentialsId: 'secret_id', variable: 'npm_token')]) {
                        echo "${npm_token}"
                    }
                    def token = 'a123532='
                    echo "asdf${token$}"
                }
                
            }
        }

        // stage('publish') {
        //     steps {
        //         script {
        //                 sh "npm whoami"

        //                 newVersion = generateReleaseVersion("pr")
        //                 sh "npm pkg set version=${newVersion}"

        //                 if (!isVersionDuplicated(newVersion)){
        //                     try{
        //                         sh "npm publish"
        //                     }catch(error){
        //                         sh "echo 'DEPLOY ABORTED WITH ERROR' ${error}"
        //                     }
        //                 } else {
        //                     sh "echo '**PUBLISHIN SKIPPED** REASON: Version ${newVersion} already exists '"
        //                 }
                        
        //         }
        //     }
        // }

        // stage('post'){
        //     steps {
        //         sh "echo 'postmessage'"
        //     }
        // }
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

def isVersionDuplicated(version){
    //def version = sh(script: "node -p -e \"require('./package.json').version\"" , returnStdout: true)
    
    try{
        def output = sh(script: """npm view aa2-package@${version}""", returnStdout:true )
        echo "${output}"
        return (output.length() == 0) ? false : true
    }catch(error) {
        sh "echo catch false"
        return false
    }
}