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
                git branch: 'main', credentialsId: '6fa4c8a9-14a9-44e0-8630-b540766d146d', url: 'https://github.com/manojsubramaniam/test02.git'

            }
        }
	stage('Docker Container Clean'){
            steps {
                sh 'docker system prune -a --volumes -f'
		sh'docker rm -f samplecont'
		sh'docker rmi -f samplecont'
	    }
        }
        stage('Docker Container'){
            steps {
                sh 'docker-compose up -d --build'
            }
        }
	stage('File Deployment'){
            steps{
                sh 'docker cp staticwebsite.html samplecont:/usr/share/nginx/html/index.html'
            }
	}
    }
}
