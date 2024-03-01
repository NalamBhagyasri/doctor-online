pipeline{
    agent any
    stages{
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
    post {
        success {
            echo "Successfully implemented"
        }
        failure {
            echo "this job is failed"
        }
    }
}
 

