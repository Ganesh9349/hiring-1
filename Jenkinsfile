pipeline{
    agent any
        stages{
           
            stage("maven build"){
              
            steps{
              sh 'mvn clean package'
            }
        }
        stage('docker build'){
          
            steps{
               sh "docker build -t bangodi/hiring:0.0.2 ."
            }
        }
            stage('docker push'){
               
                steps{
                    withCredentials([string(credentialsId: 'hub-p', variable: 'dubpwd')])
                    sh "docker -u bangodi -p ${dubpwd}"
                    sh "docker push bangodi/hiring:0.0.2"
                      }
                }
             }
     stage('docker deploy'){
               
                steps{
                    shagent(['docker-host']) {
                     }
                 }
             }
   
         }
    }
