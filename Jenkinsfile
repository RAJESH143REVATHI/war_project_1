node
{
def mavenHome = tool name: "apache-maven-3.8.8"
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '4')), pipelineTriggers([pollSCM('* * * * *')])])

echo "The job name is: ${env.JOB_NAME}"

stage('checkoutCode'){
git credentialsId: 'github_New', url: 'https://github.com/RAJESH143REVATHI/war_project_1.git'    
}
stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
/*
stage('SonarQube'){
sh "${mavenHome}/bin/mvn sonar:sonar"
}
*/
stage("DeployArtifacts into nexus"){
sh "${mavenHome}/bin/mvn deploy"    
}
stage('tomcat'){
sshagent(['f346c79f-38a0-4c16-bffb-632546e8cf75']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-app.war ubuntu@13.127.228.16:/opt/tomcat9/webapps"
}    
}


}
