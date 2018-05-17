node {
    
    // 'try-catch' blocks allow sending notifications on build failures.
    try {
        
        // Build job should be run on clean workspace, unless there is a reason not to clean it up.
        stage('Cleanup Workspace') {
            step([$class: 'WsCleanup'])
        }
        // Providing credentials for TimeTrade Docker registry.
        withDockerRegistry([credentialsId: 'cd78e3ef-ca0f-4eb8-94c6-336ba858e125', url: 'https://docker.ttops.net']) {
            
            // Defining image from TimeTrade Docker registry for container that we're building Java components with.
            // Selecting 'jenkins' user and mounting SSH keys directory from host under 'jenkins' user's home directory
            // in container to be able create release tag on GitHub via SSH.
            docker.image('docker.ttops.net/java:8u144-jdk').inside('--user jenkins ' +
                                                                   '--volume /var/lib/jenkins/.ssh:/var/lib/jenkins/.ssh:ro') {
                    // Since 'Jenkinsfile' is in a GitHub repo, repository URL is implicit so can simply call checkout scm.
                    stage('Checkout') {
                        checkout scm
                    }  
            }
        }        
    }
    catch(e) {
        throw e
    }
}
