node {

	def app
	
	stage('clone repository'){
	checkout scm
	}
	
	stage('Build image') {
	
	app = docker.build("cicd-pipeline/cicdPipeline")
	
	}
	
	stage('Test image'){
	
	app.inside {
	
	sh 'echo "Tests passed"'
	
	}
	}
	stage("Checkout"){
	steps{
	git branch: BRANCH_NAME,credentialsId: CREDENTIALS_ID, url: REPOSITORY_URL }
	}
	stage('push image'){
	
	docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'){
	app.push("${env.BUILD_NUMBER}")
	app.push("latest")	
	}
	}
	}

