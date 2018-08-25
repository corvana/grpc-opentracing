#!/usr/bin/env groovy

// Use the default version of the jenkins-pipelines plugin
@Library("corvana-jenkins-pipelines") _

pods.standard {
  checkout scm

  dir('java') {
    stage('Build') {
      gradle.call('-Dcorvana.nexus.baseurl=http://nexus-nexus:8081 build')
    }

    if (currentBuild.result == null || currentBuild.result == 'SUCCESS') {
      stage('uploadArchives') {
        gradle.call('-Dcorvana.nexus.baseurl=http://nexus-nexus:8081 uploadArchives')
      }
    }
  }
}

