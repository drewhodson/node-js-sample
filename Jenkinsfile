@Library('shared-libraries@phase1')_

node {
    setupEnvironment()

    try {
      checkoutSourceCode()
      installDependencies()
      testApplication()
      packageApplication()
      deployToHeroku appName: 'mszewczyk-node-js-sample-1'
    } finally {
      deleteDependencies()
    }
}