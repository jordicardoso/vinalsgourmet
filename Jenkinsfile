pipeline {
    agent any
    
    stages {
	stage ('build') {
	    steps{		
		sh "hugo -D -F -b http://vg.vinals.local"
	    }
	}
	stage ('deploy') {
	    steps{
		sh 'rsync -r "$WORKSPACE/public/" git@172.26.0.14:/opt/docker/hugo/vg/public/'
		gitlog()
   		slackSend color: '#1e602f', message: ":thumbsup_all: - Deployment to production: PROJECT - ${env.JOB_NAME} - Build Number - ${env.BUILD_NUMBER} - (${GIT_COMMIT})"
	    }
	}

    }
}

def gitlog() {
    sh('git log -1 --pretty=%B > commit-log.txt')
    GIT_COMMIT=readFile('commit-log.txt')    
}