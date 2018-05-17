node {  
    // 'try-catch' blocks allow sending notifications on build failures.
    try {       
        // Build job should be run on clean workspace, unless there is a reason not to clean it up.
        stage('Cleanup Workspace') {
            step([$class: 'WsCleanup'])
        }    
	withCredentials([[$class          : 'UsernamePasswordMultiBinding',
                          credentialsId   : 'jenkins-artifactory-access-token',
                          usernameVariable: 'ARTIFACTORY_USERNAME',
                          passwordVariable: 'ARTIFACTORY_TOKEN']]) {
                    // Since 'Jenkinsfile' is in a GitHub repo, repository URL is implicit so can simply call checkout scm.
          stage('Checkout') {
            checkout scm
          }
	}
      }        
    catch(e) {
        throw e
    }
}
