pipeline {
    agent any
    environment {
        GIT_LATEST_COMMIT_EDITOR= sh(
            returnStdout:true,
            script: 'git show -s --pretty=%cn '
        ).trim()
        GIT_SSH_URL = sh(
            returnStdout: true,
            script: "git config --get remote.origin.url | sed 's/https:\\/\\/github.com\\//git@github.com:/g'"
        )
        GIT_CURRENT_BRANCH = sh(
            returnStdout: true,
            script: "git rev-parse --abbrev-ref HEAD"
        )
        HOME = '.'
	  }


    stages {
        stage ('Show commit author') {
            steps {
                sh "echo '${env.GIT_LATEST_COMMIT_EDITOR}'"
            }
        }
    
        stage ('npm install'){
             steps {
                        sh "npm install"
                    }
                }
        stage('NPM build'){
                    steps {
                        sh 'npm run start:dev'
                    }
                }
         stage ('Test') {
                    steps {
                        sh 'curl localhost:3000'
                        
                    }
                }
    }    
}

