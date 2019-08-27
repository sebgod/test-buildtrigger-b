pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'This is build B'
        sh 'uname -a'
        
        script {
          currentBuild.getBuildCauses()?.each { c -> echo "[INFO] ${currentBuild.getFullDisplayName()} (current): Cause: ${c}" }
          
          def manualTrigger = true
          currentBuild.upstreamBuilds?.each { b ->
            echo "[INFO] Upstream build: ${b.getFullDisplayName()}"
            b.getBuildCauses()?.each { c -> echo "[INFO] ${b.getFullDisplayName()}: Cause: ${c}" }
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
