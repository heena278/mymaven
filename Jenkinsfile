    
    
    
    
    
    pipeline
{
    agent any
    stages
    {
        stage('contdownload')
        {
            steps
            {
               git 'https://github.com/heena278/mymaven.git'
            }
        }
        stage('contbuild')
        {
            steps
            {
                 sh 'mvn package'
            }
        }
        stage('contdeploy')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'e891992c-4cc3-4374-ab75-1ef882884f4c', path: '', url: 'http://172.31.42.124:8080')], contextPath: 'testapp', war: '**/*.war'


            }
        }
        stage('conttesting')
        {
            steps
            {
                
              git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
              
                sh 'java -jar /var/lib/jenkins/workspace/declarativepipeline2/testing.jar'
            }
        }
        stage('contdelivery')
        {
            steps
            {
                input message: 'need approval from dm', submitter: 'srinivas'
                deploy adapters: [tomcat9(credentialsId: 'e891992c-4cc3-4374-ab75-1ef882884f4c', path: '', url: 'http://172.31.39.79:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
