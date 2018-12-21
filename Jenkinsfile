pipeline {
	agent none
	stages {
		stage('Build') {
			agent any
			steps {
				// https://jenkins.io/blog/2016/10/16/stage-lock-milestone/
				// The first milestone step starts tracking concurrent build order
				milestone label: 'build', ordinal: 1
				echo 'compiling...'
				sh 'touch a.jar'
				stash includes: 'a.jar', name: 'myApp'
			}
		}
		stage('Test') {
			agent any
			steps {
				unstash 'myApp'
				echo 'testing...'
			}
		}
		stage('Performance Regression Analysis') {
 			when { not { branch 'master' } }
			agent { label 'dedicatedPerformanceMachine' }
			steps {
				unstash 'myApp'
				echo 'testing...'
			}
		}
		stage('Approval') {
			when { branch 'master' }
			// no agent is used, so executors are not used up when waiting for approvals
			agent none
			steps {
				checkpoint 'ready for approval'
				script {
					def approver = input id: 'Deploy', message: 'Deploy to production?', submitter: 'rkivisto,admin', submitterParameter: 'deploy_approver'
					echo "This deployment was approved by ${approver}"
				}
				// This milestone will abort all older builds than this one
				// so old builds don't get deployed to production
				milestone label: 'deploy', ordinal: 2
			}
		}
		stage('Deploy') {
			when { branch 'master' }
			agent any
			steps {
				lock(resource: 'deployApplication'){
					unstash 'myApp'
					echo 'Deploying...'
				}
			}
		}
	}
}
