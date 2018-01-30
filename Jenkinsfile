#!/usr/bin/groovy

//load pipeline functions
// Requires pipeline-github-lib plugin to load library from github
@Library('github.com/campbelldgunn/jenkins-pipeline')
def pipeline = new org.whiteshieldinc.Pipeline()

podTemplate(label: 'jenkins-pipeline', nodeSelector: 'os=linux', containers : [
    containerTemplate(name: 'jnlp', image: 'jenkinsci/jnlp-slave:3.14-1-alpine', orgs: '${computer.jnlpmac} ${computer.name}', workingDir: '/home/jenkins', resourceRequestCpu: '200m', resourceLimitCpu: '200m', resourceRequestMemory: '256Mi', resourceLimitMemory: '256Mi'),
    containerTemplate(name: 'docker', image: 'docker:17.10.0', command: 'cat', ttyEnabled: true)
],
volumes:[
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
]){

    node('jenkins-pipeline') {

        def pwd = pwd()

        checkout scm

        // read in required jenkins workflow config values
        def inputFile = readFile('Jenkinsfile.json')
        def config = new groovy.json.JsonSlurperClassic().parseText(inputFile)
        println "pipeline config ==> ${config}"

        // continue only if pipeline enabled
        if (!config.pipeline.enabled) {
            println "pipeline disabled"
            return
        }
    pipeline.gitEnvVars()

    def acct = pipeline.getContainerRepoAcct(config)
    def tags = pipeline.getContainerTags(config)

    stage ('build container') {
      container('docker') {

        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: config.container_repo.jenkins_creds_id,
                        usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
          sh "docker login -u ${env.USERNAME} -p ${env.PASSWORD} dfsacr.azurecr.io"
        }

        pipeline.containerBuildPub(
            dockerfile: config.container_repo.dockerfile,
            host      : config.container_repo.host,
            acct      : acct,
            repo      : config.container_repo.repo,
            tags      : tags,
            auth_id   : config.container_repo.jenkins_creds_id
        )
      }
    }
  }
}
