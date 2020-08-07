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
          sh 'scp -r root@54.224.107.68:~/var/lib/jenkins/workspace/givecharity_master/target/*.jar root@107.23.23.98:~/home/ubuntu/opt/deployment/backend'
        // excuting jar command 
          sh 'ubuntu@107.23.23.98 "nohup java -jar /home/ubuntu/opt/deployment/backend/*.jar &"'
        } // script
      } // steps
    } // stage
     
  
 } // Stagging

 } // pipeline
