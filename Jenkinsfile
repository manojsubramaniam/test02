pipeline{
	agent any 
	
    parameters {
           	 choice(name: 'BranchName', choices:['main','branch01','branch02'], description: 'to refresh the list, go to configure, disable "this build has parameters", launch build (without parameters)to reload the list and stop it, then launch it again (with parameters)')
	}
	
    stages{
        stage("Run Tests") {
            steps {
                sh "echo SUCCESS on ${BranchName}"
            }
        }
        stage('Checkout') {
            steps{
                git branch: 'main', credentialsId: '1705ca28-2134-443e-972b-a7c033df50d1', url: 'https://github.com/manojsubramaniam/test02.git'

            }
        }
        stage('Docker Container'){
            steps {
                sh '''
                    docker system prune -a --volumes -f
                    docker compose up -d
                    docker compose ps
                   '''
            }
        }
	stage('File Deployment'){
            steps{
                sh 'docker cp staticwebsite.html samplecont:/usr/share/nginx/html/index.html'
            }
	}
    }
}
