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
          sh 'scp -r ubuntu@/3.235.161.70:~/var/lib/jenkins/workspace/givecharity_master/target/*.jar ubuntu@3.235.9.10:~/opt/deployment/backend'
        // excuting jar command 
          sh 'ubuntu@3.235.9.10 "nohup java -jar /home/appuser/opt/deployment/backend/*.jar &"'
        } // script
      } // steps
    } // stage
     
  
 } // Stagging

 } // pipeline
