node
{
 
 def mavenHome = tool name: "maven3.8.4"
 stage('CheckoutCode')
 {
 git branch: 'development', credentialsId: 'aa1ea2c6-1508-4987-bd3c-0f996086ce0b', url: 'https://github.com/Shanthi-3452/maven-web-application.git'
 }
 
 stage('Build'){
 sh "${mavenHome}/bin/mvn clean package"
 }
 
 stage('ExecuteSonarQubeReport'){
 sh "${mavenHome}/bin/mvn sonar:sonar"
 }
 
 stage('UploadArtifactIntoNexus'){
 sh "${mavenHome}/bin/mvn deploy"
 }
 
 stage('DeployAppintoTomcat'){
 sshagent(['d496b35c-7162-4146-96d8-0349729c981d']){
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.7.68.182:/opt/apache-tomcat-9.0.56/webapps/"
 }
 
 }
 stage('SendNotifications'){
 emailext body: '''Build Over,

 Regards,
 Chandra Technologies,
 9986998659''', subject: 'Build Over..', to: 'chandrabrand3452@gmail.com'
 }
 
} 
