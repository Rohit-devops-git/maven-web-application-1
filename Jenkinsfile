node{

def mavenHome = tool name: "maven3.8.4"

//Get the code from Github Repo
stage('CheckoutCode'){
git branch: 'development', credentialsId: '256be0c9-acb4-4c7a-a687-dff5fcabfeaa', url: 'https://github.com/Rohit-devops-git/maven-web-application-1.git'
}

//Using Maven

 stage('Build'){
 sh "${mavenHome}/bin/mvn clean package" 
}

 stage('Execute SonarQubeReport'){
 sh "${mavenHome}/bin/mvn sonar:sonar"
}

 stage('Upload ArtifactIntoNexusRepo'){
 sh "${mavenHome}/bin/mvn deploy"
}
 stage('DeployAppintoTomactServer')
 {
 sshagent(['4cfc1523-04a4-4e10-8beb-32df9f94b24d']){
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.110.45.95:/opt/apache-tomcat-9.0.58/webapps/"
}
 
}

}//Node Closed
