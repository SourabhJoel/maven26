pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/SourabhJoel/maven26.git'
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
                sh  '''scp /var/lib/jenkins/workspace/PipelinebySCM/webapp/target/webapp.war ubuntu@172.31.28.30:/var/lib/tomcat9/webapps/testapp.war'''
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/MyDecJob/testing.jar'
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '74b04562-42e6-4d24-9e87-d1f08f450c4d', path: '', url: 'http://172.31.24.172:8080')], contextPath: 'testapps', war: '**/*.war'
            }
        }
    }
}
