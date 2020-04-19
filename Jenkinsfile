pipeline{
    agent any
	enviroment {
    tomcat_Host="ec2-user@172.31.36.236"
	tomcat_svc="usr/sbin/service tomcat"
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
          sh "ssh ${tomcat_Host} ${tomcat_svc} stop"
          sh "ssh ${tomcat_Host} ${tomcat_svc} start"
}
        }
        }
        }
}