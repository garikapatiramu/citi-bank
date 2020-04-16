pipeline{
    agent any
    stages{
        stage ("git checkout")
        {
        steps{
            git branch:'develop',
            credentialsId: 'github', 
            url: 'https://github.com/garikapatiramu/citi-bank'
        }
        }
        stage (" maven package and  nexus deploy")
        {
        steps{
          sh script: 'mvn clean deploy'
        }
        }
        stage ("Tomact-dev")
        {
        steps{
          echo "need to deploy the file in tomcat"
        }
        }
        }
}
