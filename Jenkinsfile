@Library('shared-libraries@phase1')_

node {
    setupEnvironment()

    try {
      checkoutSourceCode()
      installDependencies()
      testApplication()
      packageApplication()
      deployToHeroku appName: 'warm-hollows-29053'
    } finally {
      deleteDependencies()
    }
}