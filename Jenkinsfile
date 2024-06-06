pipeline {
    agent any
	
	tools {
    jdk 'java 1.8'

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
		
		stage('Deploy to tomcat') {
            steps {
                echo 'Deploying artifact to tomcat webserver '
				deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://54.167.199.250:8081/')], contextPath: 'googlepage2', war: '**/*.war'
            }
        }
    }
}
