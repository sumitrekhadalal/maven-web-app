pipeline{
    agent any
    environment {
        PATH = "$PATH:/opt/apache-maven-3.6.3/bin"
    }
    stages{
       stage('GetCode'){
            steps{
				git branch: 'main',
                url: 'https://github.com/ashokitschool/maven_web_app_jenkins_pipeline.git'
            }
         }        
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
         }   
        stage('deploy'){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcatserver', path: '', url: '')], contextPath: 'http://172.31.35.219:8080', war: '**/*.war'
            }
         }      
    }
}
