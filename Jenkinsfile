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
          sh 'scp -r jenkins@54.236.62.208:~/var/lib/jenkins/workspace/givecharity_master/target/*.jar appuser@3.237.195.201:~/opt/deployment/backend'
        // excuting jar command 3.237.195.201
          sh 'appuser@3.237.195.201 "nohup java -jar /home/appuser/opt/deployment/backend/*.jar &"'
        } // script
      } // steps
    } // stage
     
  
 } // Stagging

 } // pipeline
