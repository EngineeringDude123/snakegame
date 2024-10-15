node ('New-Appserver') 
{
	def app	
	stage('Cloning git')
	{
		checkout scm
	}

	
	stage ('Build-and-tag')
	{
		app = docker.build("johncoll/snake_game_2024")
	}


	stage ('Post-to-Dockerhub')
	{
		docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
		{
			app.push("latest")
		}
	}


	stage ('pull-image-server')
	{
		sh "docker-compose down"
		sh "docker-compose up -d"
	}
	
}