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
                git branch: 'main', credentialsId: '30d20ff5-3d97-4aaa-a4da-111ae90beac8', url: 'https://github.com/manojsubramaniam/test02.git'

            }
        }
        stage('Docker Container'){
            steps {
                sh 'docker compose up -itd'
            }
        }
	stage('File Deployment'){
            steps{
                sh 'docker cp staticwebsite.html samplecont:/usr/share/nginx/html/index.html'
            }
	}
    }
}
