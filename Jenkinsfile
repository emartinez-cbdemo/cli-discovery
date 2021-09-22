library 'pipeline-library'
pipeline {
  agent none
  options {
    timeout(time: 10, unit: 'MINUTES')
    buildDiscarder(logRotator(numToKeepStr: '2'))
  }
  stages {
    stage("Discover CLI") {
      agent { label 'default-jnlp' } 
      when {
        branch 'main'
      }
      steps {
        withCredentials([usernamePassword(credentialsId: 'admin-cli-token', usernameVariable: 'JENKINS_CLI_USR', passwordVariable: 'JENKINS_CLI_PSW')]) {
          sh """
            curl -O http://emartinez-20210921-emartinez-demo-controller/emartinez-20210921-emartinez-demo-controller/jnlpJars/jenkins-cli.jar
            alias cli='java -jar jenkins-cli.jar -s http://emartinez-20210921-emartinez-demo-controller/emartinez-20210921-emartinez-demo-controller/ -auth $JENKINS_CLI_USR:$JENKINS_CLI_PSW'
            cli help
          """
        }
      }
    }
  }
}
