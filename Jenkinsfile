pipeline{
    agent any
	enviroment{
	tomcat_user="ec2-user"
	tomcat_Host="${tomcat_user}@172.31.36.236"
	tomcat_service='usr/sbin/service tomcat'
	}
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
          // copy citi bank war file to tomcat server
          sh "scp -o StrictHostKeyChecking=no  target/citi-bank.war ${tomcat_Host}:/opt/tomcat8/webapps/"
          sh "ssh {tomcat_Host} ${tomcat_service} stop"
          sh "ssh {tomcat_Host} ${tomcat_service} start"
}
        }
        }
        }
}