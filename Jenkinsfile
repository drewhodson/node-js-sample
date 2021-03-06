node {
    env.NODEJS_HOME = "${tool 'NodeJS'}"
    env.PATH="${env.NODEJS_HOME}/bin:${env.PATH}"

    try {
        stage('Checkout source code') {
            checkout scm
        }
        
        stage('Install dependencies') {
            echo 'Installing dependencies...'
            sh 'npm install'
        }
        
        stage('Package application') {
            echo 'Packaging application...'
            sh 'npm pack'
        }
        
        stage('Deploy to Heroku') {
          if (env.TAG_NAME) {
            echo 'Deploying to Heroku...'
            withCredentials([usernamePassword(credentialsId: 'heroku', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                sh "git push https://${USERNAME}:${PASSWORD}@git.heroku.com/warm-hollows-29053.git ${env.TAG_NAME}:master"
            }
          } else {
            echo 'Not a release. Skipping deployment.'
          }
        }
    } finally {
        stage('Deleting dependencies') {
            echo 'Deleting dependencies...'
            cleanWs patterns: [[
                    pattern: 'node_modules',
                    type: 'INCLUDE'
                ]],
                deleteDirs: true
        }
    }
}