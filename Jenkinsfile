pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'ad06371d-2401-4512-a146-74e00a82f774', path: '', url: 'http://172.31.49.199:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
         stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'ad06371d-2401-4512-a146-74e00a82f774', path: '', url: 'http://172.31.57.186:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
