@Library('piper-library-os') _
node() {
    stage('prepare') {
	deleteDir()
        checkout scm
        setupCommonPipelineEnvironment script:this
    }
    stage('Build') {
        mtaBuild script: this
    }
    stage('deploy') {
        cloudFoundryDeploy script: this
        slackSendNotification script: this
    }
}
