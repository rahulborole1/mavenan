pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/rahulborole1/mavenan.git'
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
                deploy adapters: [tomcat9(credentialsId: 'a6c49834-9973-4c10-813f-673286d5d0bc', path: '', url: 'http://172.31.22.61:8080')], contextPath: 'qaapp', war: '**/*.war'
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
      
        stage('ContinuosuDelivery')
        {
            steps
            {
              input message: 'Required Approval from the DM!', submitter: 'sai'
              deploy adapters: [tomcat9(credentialsId: 'a6c49834-9973-4c10-813f-673286d5d0bc', path: '', url: 'http://172.31.24.43:8080')], contextPath: 'myprodapp', war: '**/*.war'
            }
        }
        
        
    }
}

