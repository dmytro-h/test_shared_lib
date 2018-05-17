node {  
    // 'try-catch' blocks allow sending notifications on build failures.
    try {
        
        // Build job should be run on clean workspace, unless there is a reason not to clean it up.
        stage('Cleanup Workspace') {
            step([$class: 'WsCleanup'])
        }
	withCredentials( getArtifactoryCredentials() ) {
	  stage('Get file') {
	    sh 'touch test_file-$BUILD_NUMBER'
            sh 'echo "test_text" > test_file-$BUILD_NUMBER'
	  }
					
	  stage('Upload to Artifactory test_folder') {
	    uploadArtifactory('test_file-$BUILD_NUMBER', 'for_testing_cleanup/test_folder/')
	  }
	 }
        }        
    catch(e) {
        throw e
    }
}
