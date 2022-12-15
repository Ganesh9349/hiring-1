pipeline{
    agent any
        stages{
        stage("git check out"){
            steps{
               git branch: 'main', credentialsId: 'git-creds', url: 'https://github.com/Ganesh9349/hiring-1'
            }
        }
        stage("maven build"){
            steps{
              sh 'mvn clean package'
            }
        }
        stage("tomcat"){
            steps{
                sshagent(['tomcat-creds']) {
                   // copy war
                   sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.90.212:/opt/tomcat9/webapps"
                   // stop war
                   sh "ssh ec2-user@172.31.90.212 /opt/tomcat9/bin/shutdown.sh"
                   // start war
                   sh "ssh ec2-user@172.31.90.212 /opt/tomcat9/bin/startup.sh"
                }
            }
        }
    }
}
