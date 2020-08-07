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
          sh 'scp jenkins@3.236.162.51:~/var/lib/jenkins/workspace/givecharity/target/*.jar ubuntu@3.236.185.64:/home/ubuntu/opt/deployment/backend'
        // excuting jar command 
          sh 'ubuntu@3.236.185.64 "nohup java -jar /home/ubuntu/opt/deployment/backend/*.jar &"'
        } // script
      } // steps
    } // stage
     
  
 } // Stagging

 } // pipeline
