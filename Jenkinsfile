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
	    stage('nexus'){
            steps{
                nexusArtifactUploader credentialsId: 'nexus', groupId: 'mavan2', nexusUrl: '13.233.154.144:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'sumit-1st-artifact', version: ''
            }
         }
	    stage('deploy'){
		    steps{
                        deploy adapters: [tomcat9(credentialsId: 'tomcatserver', path: '', url: 'http://13.233.107.127:8080/')], contextPath: '/', war: '**/*.war'
		    }    
		 }
           }		    
     }
