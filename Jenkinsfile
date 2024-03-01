pipeline{
    agent any
    stages{
        stage("checkout"){
            steps{
                git branch: 'main', url: 'https://github.com/NalamBhagyasri/doctor-online'
            }
        }
        stage("build"){
            steps{
                sh 'mvn package'
            }
        }
        stage("deploy"){
            steps{
                sshagent(['tomcat-dev']){
                    //copy war file tpo tomcat server
                    sh "scp -o StrictHostKeyChecking=no target/doctor-online.war ec2-user@172.31.46.229:/opt/tomcat10/webapps/"
                    //restart tomcat server
                    sh "ssh ec2-user@172.31.46.229 /opt/tomcat10/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.46.229 /opt/tomcat10/bin/startup.sh"
                }
            }
        }
    }
}
