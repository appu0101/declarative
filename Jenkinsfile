pipeline
{
    agent any 
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/appu0101/declarative.git'
            }
            
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
            
        }
        stage('ContinuousDeployment')
        {
            steps
            {
               deploy adapters: [tomcat9(credentialsId: 'f8bdd284-8d4a-460b-bc2b-9544f29f0207', path: '', url: 'http://172.31.88.115:8080')], contextPath: 'testapp', war: '**/*.war'
            }
            
        }
        stage('ContinuousTesting')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
               sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
            }
            
        }
        stage('ContinuousDelivery')
        {
            steps
            {
               input message: 'Need Approval', submitter: 'Ravi'
               deploy adapters: [tomcat9(credentialsId: 'f8bdd284-8d4a-460b-bc2b-9544f29f0207', path: '', url: 'http://172.31.87.155:8080')], contextPath: 'prodapp', war: '**/*.war'
               
            }
            
        
        }
    }
}
