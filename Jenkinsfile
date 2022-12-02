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
                        nexusArtifactUploader artifacts: [[artifactId: 'webapp-any', classifier: '', file: '/var/lib/jenkins/workspace/new1/target/01-maven-web-app.war', type: 'war']], credentialsId: 'nexus', groupId: 'webapp-any', nexusUrl: '65.1.95.245:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'sumit-1st-artifact', version: '1.0-SNAPSHOT'         }
	    stage('deploy'){
		    steps{
                        deploy adapters: [tomcat9(credentialsId: 'tomcatserver', path: '', url: 'http://13.233.107.127:8080/')], contextPath: '/', war: '**/*.war'
		    }    
		 }
           }		    
     }
