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
                    def deploymentDelay = input id: 'Delpoy for stagging', message: 'Deploy to stagging?', submitter: 'rkivisto,admin', parameters: [choice(choices: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24'], description: 'Hours to delay deployment?', name: 'deploymentDelay')]
                    sleep time: deploymentDelay.toInteger(), unit: 'HOURS'
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
