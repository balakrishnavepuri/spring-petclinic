pipeline {

  agent { label 'master' }

  options {

    disableConcurrentBuilds()
    timeout(time: 10, unit: 'MINUTES')
    buildDiscarder(logRotator(numToKeepStr: '10'))

  } 


 stages {
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }





stage('Approval') {
            // no agent, so executors are not used up when waiting for approvals
            agent none
            steps {
                script {
                    emailext mimeType: 'text/html',
                 subject: "[Jenkins]${currentBuild.fullDisplayName}",
                 to: "balakrishnavepuri@gmail.com",
                 body: '''<a href="${BUILD_URL}input">click to approve</a>'''

        def userInput = input id: 'userInput',
                              message: 'Let\'s promote?', 
                              submitterParameter: 'submitter',
                              submitter: 'balakrishna',
                              parameters: [
                                [$class: 'TextParameterDefinition', defaultValue: 'stagging', description: 'Environment', name: 'env'],
                                [$class: 'TextParameterDefinition', defaultValue: 'Stagging_Server', description: 'Target', name: 'target']]

        echo ("Env: "+userInput['env'])
        echo ("Target: "+userInput['target'])
        echo ("submitted by: "+userInput['submitter'])
                }
            }
        }


// Stagging_Environment
stage('Delpoy for stagging') {
            when {
                branch 'master'
            }
            steps {
                script {
            //enable remote triggers
          properties([pipelineTriggers([pollSCM('* * * * *')])])
          // copying jar file to Stagging Server
          sh 'scp -r /var/lib/jenkins/workspace/givecharity_master/target/*.jar ubuntu@34.201.48.214:/opt/deployment/backend'
        // excuting jar command 3.237.195.201
          sh 'ssh ubuntu@34.201.48.214 "nohup java -jar /opt/deployment/backend/*.jar &"'
        } // script
      } // steps
    } // stage
     
  
 } // Stagging


 } // pipeline
