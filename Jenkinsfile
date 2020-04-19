pipeline{
    agent any
	environment {
        TOMCAT_USR = "ec2-user"
        TOMCAT_HOST = "${TOMCAT_USR}@172.31.36.236"
        TOMCAT_SVC = "/usr/sbin/service tomcat"
    }
	stages{
        stage (" maven package and  nexus deploy")
        {
        steps{
          sh script: 'mvn clean deploy ramu'
        }
        }
        stage ("Tomact-dev")
        {
        steps{
          sshagent(['tomcat']) {
          // copy citi bank war file to tomcat server
          sh "scp -o StrictHostKeyChecking=no  target/citi-bank.war ${TOMCAT_HOST}:/opt/tomcat8/webapps/"
          sh "ssh ${TOMCAT_HOST} ${TOMCAT_SVC} stop"
          sh "ssh ${TOMCAT_HOST} ${TOMCAT_SVC} start"
}
        }
        }
        }
		
		post {
  failure {
    // One or more steps need to be included within each condition's block.
	echo "send email notifications"
  }
}
}