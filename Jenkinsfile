pipeline
{
  agent none
 
  stages
  {
    stage('CLONE GIT REPOSITORY')
    {
      agent
      {
        label 'Ubuntu-Appserver-3120'
      }
      steps
      {
        checkout scm
      }
    }
 
    stage('SCA-SAST-SNYK-TEST')
    {
      agent
      {
        label 'Ubuntu-Appserver-3120'
      }
      steps
      {
        echo "SNYK-TEST"
      }
    }
 
     stage('BUILD-AND-TAG')
    {
      agent
      {
        label 'Ubuntu-Appserver-3120'
      }
      steps
      {
         script
         {
            def app = docker.build("johncoll/snakegame")
            app.tag("latest")
         }
      }
    }
 
      stage('POST-TO-DOCKERHUB')
    {
      agent
      {
        label 'Ubuntu-Appserver-3120'
      }
      steps
      {
         script
         {
            docker.withRegistry("https://registry.hub.docker.com", "dockerhub_credentials")
            {
                def app = docker.image("johncoll/snakegame")
                app.push("latest")
 
            }
           
         }
      }
    }
 
    stage('DEPLOYMENT')
    {
      agent
      {
        label 'Ubuntu-Appserver-3120'
      }
      steps
      {
        sh "docker-compose down"
        sh "docker-compose up -d"
      }
    }
 
   
   
  }
 
}