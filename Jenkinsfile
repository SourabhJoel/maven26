pipeline
{
    agent any
    stages
    {
        stage ("ContinuousDownload")
        {
            steps
            {
                git 'https://github.com/SourabhJoel/maven26.git'
            }
        }
        stage ("ContinuousBuild")
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage ("ContinuousDeployment")
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '863eb6ef-0c27-4e2b-9ea8-fc582bcb3231', path: '', url: 'http://172.31.21.72:8080')], contextPath: 'Testapp', war: '**/*.war'
            }
        }
        stage ("ContinuousTesting")
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipelineJob/testing.jar'
            }
        }
        stage ("ContinuousDelivery")
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '863eb6ef-0c27-4e2b-9ea8-fc582bcb3231', path: '', url: 'http://35.88.143.90:8080')], contextPath: 'Prodapp', war: '**/*.war'
            }
        }
    }
}
