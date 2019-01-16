def branch = '02-simple-pipeline'

node {
    env.NODEJS_HOME = "${tool 'NodeJS'}"
    env.PATH="${env.NODEJS_HOME}/bin:${env.PATH}"

    try {
        stage('Checkout source code') {
            git branch: branch, url: 'https://github.com/mszewczyk/node-js-sample/'
        }
        
        stage('Install dependencies') {
            echo 'Installing dependencies...'
            sh 'npm install'
        }

        stage('Test application') {
          echo 'Testing application...'
          sh 'npm test'
        }
        
        stage('Package application') {
            echo 'Packaging application...'
            sh 'npm pack'
        }
        
        stage('Deploy to Heroku') {
          echo 'Deploying to Heroku...'
          withCredentials([usernamePassword(credentialsId: 'heroku', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
              sh "git push -f https://${USERNAME}:${PASSWORD}@git.heroku.com/dehodson-node-js-sample.git ${branch}:master"
          }
        }
    } finally {
        stage('Deleting dependencies') {
            echo 'Deleting dependencies...'
            cleanWs patterns: [
                  [
                    pattern: 'node_modules',
                    type: 'INCLUDE'
                  ],
                  [ 
                    pattern: '*.tgz',
                    type: 'INCLUDE'
                  ]
                ],
                deleteDirs: true
        }
    }
}