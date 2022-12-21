pipeline {
    agent any
    stages{
        stage("git repository"){
            steps{
                git branch: 'main', credentialsId: 'git-hub', url: 'https://github.com/517002/myjob'
            }
       
        }
        stage("maven package"){
            steps{
                sh 'mvn clean package'
            }
        }
        stage("tomcat deploy"){
            steps{
            sshagent(['tomcat']){
               sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.24.138:/opt/tomcat9/webapps"
               sh "ssh ec2-user@172.31.24.138 /opt/tomcat9/bin/shutdown.sh"
               sh "ssh ec2-user@172.31.24.138 /opt/tomcat9/bin/startup.sh"
               }   
            }    
        }
    }
}
