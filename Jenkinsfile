pipeline {
  agent any
  tools {nodejs "node"} 
  environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-tavchai')
    }
  stages {    
    stage('NPM Install') {
      steps {
        git branch: 'main', url: 'https://github.com/tavchai/test-api-jenkins-docker'
        sh 'npm install'
      }
    }   
    
    stage('Build Docker image') {
      steps {
        script {
          sh 'docker build -t tavchai/test-api-to-hub .'
        }
      }
    }
    
   stage('Push image to Hub') {

		steps {
			sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
		
		    sh 'docker push tavchai/test-api-to-hub'
		}
	}
    
  }
  post {
		always {
			sh 'docker logout'
		}
	}
}
