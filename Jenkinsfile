pipeline{
    agent any
    stages{
        stage (" maven package and  nexus deploy")
        {
        steps{
          sh script: 'mvn clean deploy'
        }
        }
        stage ("Tomact-dev")
        {
        steps{
          sshagent(['tomcat']) {
         
                sshagent(['tomcat-dev']) {
                    // copy war file to tomcat dev
                    sh "scp -o StrictHostKeyChecking=no  target/citi-bank*.war  ec2-user@172.31.36.236172.31.36.236:/opt/tomcat8/webapps/"
                    sh "ssh ec2-user@172.31.36.236 service tomcat stop"
                    sh "ssh ec2-user@172.31.36.236 service tomcat start"
}
        }
        }
        }
}
