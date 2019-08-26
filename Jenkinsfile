pipeline {
	agent none
	triggers {
        	cron('0 9 1-7 * 1')
    	}
	stages {
		stage('Build') {
			agent any
			steps {
				sh 'printenv'
				echo GIT_BRANCH
				sh 'echo $(git --no-pager show -s --format='%an' $GIT_COMMIT)'
				def GIT_NAME = $(git --no-pager show -s --format='%an' $GIT_COMMIT)
				def GIT_EMAIL = $(git --no-pager show -s --format='%ae' $GIT_COMMIT)
				echo GIT_EMAIL
				// https://jenkins.io/blog/2016/10/16/stage-lock-milestone/
				// The first milestone step starts tracking concurrent build order
				//milestone label: 'build', ordinal: 1
				//echo 'compiling...'
				//sh 'touch a.jar'
				//stash includes: 'a.jar', name: 'myApp'
			}
		}
		//stage('Test') {
		//	agent any
		//	steps {
		//		unstash 'myApp'
		//		echo 'testing...'
		//	}
		//}
		//stage('Approval') {
		//	// no agent is used, so executors are not used up when waiting for approvals
		//	agent none
		///	steps {
		//		checkpoint 'ready for approval'
		//		script {
		//			def approver = input id: 'Deploy', message: 'Deploy to production?', submitter: 'rkivisto,admin', submitterParameter: 'deploy_approver'
		//			echo "This deployment was approved by ${approver}"
		//		}
				// This milestone will abort all older builds than this one
				// so old builds don't get deployed to production
		//		milestone label: 'deploy', ordinal: 2
		//	}
		//}
		//stage('Deploy') {
		//	agent any
		///	steps {
		//		lock(resource: 'deployApplication'){
		//			unstash 'myApp'
		//			echo 'Deploying...'
		//		}
		//	}
		//}
	}
}
