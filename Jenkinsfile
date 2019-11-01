#!groovy

@Library('platform.infrastructure.pipelinelibrary') _


import groovy.json.JsonSlurper
import com.ebsco.platform.Cloudformation
import java.text.SimpleDateFormat

//string newAMI holds AMI id of newly created ami

nodeId = platformDefaults.getBuildNodeLabel()

node(nodeId) {
    def cloudformation = new com.ebsco.platform.Cloudformation()
    step([$class: 'WsCleanup'])

    // Checkout the repo from github
    stage('checkout') {
        checkout scm
    }
    stage('Deploy AlertManager') {
        cloudformation.createOrUpdateStack("eis-lz-ehost-devqa", "us-east-1", "AlertManager", "/cloudformation/alertman-template.yaml", "/cloudformation/alertman-parameters.json")

    }
//    stage('Deploy Prometheus') {
//       cloudformation.createOrUpdateStack("eis-aws-cm1", "us-east-1", "Prometheus", "/cloudformation/prom-template.yaml", "/cloudformation/prom-parameters.json")
//    }
}