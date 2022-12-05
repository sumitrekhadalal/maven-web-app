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
nexusArtifactUploader artifacts: [[artifactId: '01-maven-web-app', classifier: '', file: '01-maven-web-app.war', type: 'war']], credentialsId: 'nexas', groupId: 'maven-web-app', nexusUrl: '54.221.165.178:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://54.221.165.178:8081/repository/maven-web-app/', version: '1.0-SNAPSHOT'
	       }

            }
	    stage('deploy'){
               steps{
                deploy adapters: [tomcat8(credentialsId: 'tom', path: '', url: 'http://44.200.152.61:8080/')], contextPath: '/', war: '**/*.war'
		       
	       }
	  }
       
        }
}
