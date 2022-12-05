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
               nexusArtifactUploader artifacts: [[artifactId: 'maven-web-app', classifier: '', file: '/var/lib/jenkins/workspace/5-12-2022/target/01-maven-web-app.war',
						  type: 'war']], credentialsId: 'nexa', groupId: 'web-app', nexusUrl: '44.204.109.179:8081',
		       nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshot', version: '1.0-SNAPSHOT'
               }

            }
	    stage('deploy'){
               steps{
                deploy adapters: [tomcat8(credentialsId: 'tom', path: '', url: 'http://44.200.152.61:8080/')], contextPath: '/', war: '**/*.war'
		       
	       }
	  }
       
        }
}
