pipeline {
	agent any
	environment {
	def git_branch = 'master'
	def git_url = 'https://github.com/rishikant4/devops.git'
	
	def mvntest = 'mvn test '
	def mvnpackage = 'mvn clean install'
	
	def utest_url = 'target/surefire-reports/**/*.xml'
		
	def sonar_cred = 'sonar'
        def code_analysis = 'mvn clean install sonar:sonar'
		
	def nex_cred = 'nexus'
        def grp_ID = 'com.example'
        def nex_url = '43.204.111.29:8081'
        def nex_ver = 'nexus3'
        def proto = 'http'
	}
	stages {
	stage('Github Checkout') {
	steps {
	script {
	git branch: "${git_branch}", url: "${git_url}"
	echo 'Git Checkout Completed'
	}
	}
	} 
	stage('Maven Build') {
	steps {
	sh "${env.mvnpackage}"
	echo 'Maven Build Completed'
	}
	}
	stage('Unit Test & Reports Publishing') {
            steps {
                script {
                    sh "${env.mvntest}"
                    echo 'Unit Testing Completed'
                }
            }
	post {
                success {
                        junit "$utest_url"
                        jacoco()
                }
            }
}
    }
}
