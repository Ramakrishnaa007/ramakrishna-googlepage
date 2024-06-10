pipeline {
    agent any
	
	tools {
    jdk 'java 11.0'

  }

    stages {
        stage('CLONE SCM') {
            steps {
                echo 'Cloning GOOGLE HOME PAGE project code'
			git branch: 'main', url: 'https://github.com/Ramakrishnaa007/ramakrishna-googlepage.git'
            }
        }
		
		stage('SONARQUBE ANALYSIS') {
            steps {
                echo 'code inspection of  GOOGLE PAGE project code'
			      sh 'mvn clean compile sonar:sonar'    
            }
        }
		
		
		stage('Build Artifact ') {
            steps {
                echo 'generating artifact with maven build tool'
				sh 'mvn  install'
            }
        }
	
		stage('Publish to nexus') {
            steps {
                echo 'publishinig to nexus repository'
				sh 'mvn  deploy'
            }
        }
		
		stage('Deploy to tomcat') {
            steps {
                echo 'Deploying artifact to tomcat webserver '
				deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://54.146.73.44:8090/')], contextPath: 'google-page', war: '*/*.war'
            }
        }
    }
}
