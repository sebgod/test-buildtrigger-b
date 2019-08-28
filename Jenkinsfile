pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'This is build B'
        sh 'uname -a'
        
        script {
          
          env.GIT_COMMIT = checkout scm
          currentBuild.getBuildCauses()?.each { c -> echo "[INFO] ${currentBuild.getFullDisplayName()} (current): Cause: ${c}" }
          currentBuild.getBuildVariables()?.each { k, v -> echo "[INFO] ${currentBuild.getFullDisplayName()} (current): ${k}: ${v}" }
          
          def manualTrigger = true
          currentBuild.upstreamBuilds?.each { b ->
            echo "[INFO] Upstream build: ${b.getFullDisplayName()}"
            def scmCause = b.getBuildCauses(hudson.triggers.SCMTrigger$SCMTriggerCause.class)
            if (scmCause) {
              echo "[INFO] ${b.getFullDisplayName()}: Cause: ${scmCause}"
              b.getBuildVariables()?.each { k, v -> echo "[INFO] ${b.getFullDisplayName()}: ${k}: ${v}" }
            }
            
            manualTrigger = false
          }
          if (manualTrigger)
          {
              echo "[INFO] This build was triggered manually"
          }
        }
      }
    }
  }
}
