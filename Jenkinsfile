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
                deploy adapters: [tomcat8(credentialsId: 'tom', path: '', url: 'http://44.200.152.61:8080/')], contextPath: '/', war: '**/*.war'
		       
	       }
	  }
        stage('nexus'){
               steps{
                nexusArtifactUploader artifacts: [[artifactId: 'maven-web-app', classifier: '', file: 'maven-web-app', 
                type: 'maven-web-app']], credentialsId: 'nexa', groupId: 'nexus', nexusUrl: '44.204.109.179:8081',
                 nexusVersion: 'nexus3', protocol: 'http', repository: 'http://44.204.109.179:8081/repository/maven-releases/', version: '1.0'

               }

            }
        }
}
