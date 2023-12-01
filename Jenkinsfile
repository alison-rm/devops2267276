pipeline {
    agent any
		
    stages {
    	stage('Info') {
				steps {
					sh '''
						docker compose version
					'''
				}
    	}
    	stage('Build') {
				steps {
					sh '''docker compose build'''
				}
    	}
			stage('Install Dependencies') {
				agent {
					docker { image 'node:20.10.0' }
				}
				steps { 
					sh '''
							npm -v
							node -v
							npm install
					'''
				}
			}
			stage('Run Tests') {
				steps {
					echo 'e2e Tests'
					sh 'npm run test:e2e'
					
					echo 'CI Tests'
					sh 'npm run test:ci'
				}
			}
			stage('Run Application') {
				steps {
					sh 'docker compose up'
				}
			}
    }
}