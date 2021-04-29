pipeline {
    agent { label 'master'}
    tools {
        maven 'MAVEN' 
    }
    triggers {
        cron('H * * * 1-5')
    }
    stages {
        stage('scm') {
            steps {
                git branch: 'master', url:'https://github.com/balakrishnavepuri/spring-petclinic.git'        
            }
        }
        stage('build') {
            steps {
                withSonarQubeEnv('sonar-6.7.4') {
                    sh script: 'mvn clean package sonar:sonar'

                }
                
            }
        }
        
        stage('post build') {
            steps {
                junit 'gameoflife-web/target/surefire-reports/*.xml'
                archiveArtifacts 'gameoflife-web/target/*.war'
            }
        }
        stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true, credentialsId: 'SONAR_TOKEN'
              }
            }
        }
    }
    
}
