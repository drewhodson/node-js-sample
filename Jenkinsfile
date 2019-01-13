@Library('shared-libraries@phase2')
import com.dminc.GitCommit

node {
    setupEnvironment()

    try {
      GitCommit gitCommit = checkoutSourceCode()
      echo "Git commit id is ${gitCommit.id}."
      installDependencies()
      testApplication()
      packageApplication()
      deployToHeroku appName: 'warm-hollows-29053'
    } finally {
      deleteDependencies()
    }
}