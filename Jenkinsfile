pipeline{
  agent any
  stages{
    stage("Git Checkout"){
      steps{
            git credentialsId: 'github', url: 'https://github.com/maniumjayaraj/SaiJavaCode.git'
           }
          }
     stage("Maven Build"){
       steps{
            sh "/opt/maven/bin/mvn package"
             }
            }
     stage("deploy-dev"){
       steps{
          sshagent(['3.6.41.252'])  {
          sh """
          scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/jai/webapp/target/webapp.war ec2-user@3.6.41.252:/tomcat/webapps 
          ssh ec2-user@3.6.41.252 /tomcat/bin/shutdown.sh
          ssh ec2-user@3.6.41.252 /tomcat/bin/startup.sh
           """
            }
          }
        }
      }
    }
