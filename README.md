# pipeline-deployment-demo
A pipeline deployment demo making use of:
- only [specific users](https://jenkins.io/doc/pipeline/steps/pipeline-input-step/#input-wait-for-interactive-input) are allowed to deploy to production (rkivisto,admin)
- the user that approved the deployment is saved in `$approver` (eg. for logging to an auditing tool)
- builds for different commits can run in parallel, but deployment steps are single-threaded (one production deploy at a time)
- milestones to avoid older builds from being deployed on top of newer builds [Controlling the Flow with Stage, Lock, and Milestone](https://jenkins.io/blog/2016/10/16/stage-lock-milestone/)
- [checkpoints](https://www.cloudbees.com/products/cloudbees-jenkins-platform/enterprise-edition/features/checkpoints-plugin) are used to allow re-deployments of previous builds (binaries are [stash](https://jenkins.io/doc/pipeline/steps/workflow-basic-steps/#code-stash-code-stash-some-files-to-be-used-later-in-the-build)'d and [unstash](https://jenkins.io/doc/pipeline/steps/workflow-basic-steps/#code-unstash-code-restore-files-previously-stashed)'d)

a
aasdf
