pipeline {
    agent any
    
    tools { nodejs "node" }

    stages {
        stage ('install') {
            steps {
                script {
                    sh 'node -v'
                    echo "${env.test1}"
                    // withCredentials([string(credentialsId: 'secret_id', variable: 'npm_token')]) {
                    //     echo "${npm_token}"
                    // }
                    def token = 'a123532='
                    echo "${token}"
                    echo "asdfdd \$token"
                    sh "touch .npmrc"
                    
                    def username = 'Jenkins'
                    echo 'Hello Mr. ${username}'
                    echo "I said, Hello Mr. ${token}"

                    sh "echo '//ae-qa-nexus-app01:8081/content/groups/npm-all/:_auth=${token}' >> file.txt"
                    sh "cat file.txt"

                    cleanNpmrc()

                    sh "cat file.txt"
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

    post {
        always {
            cleanWs()
        }
    }
}

def cleanNpmrc() {
    sh "sed -i '2d' file.txt "
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