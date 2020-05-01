node {

stage ('SCM') {
//git clone
git 'https://github.com/balakrishnavepuri/spring-petclinic.git'

}

stage ('build the packages') {
// build the code
sh label: '', script: 'mvn package'

}
stage ('Archcaving the artifacts') {
// artifacts
archiveArtifacts 'target/*.jar'

}

}
