/* This selects the app server as the place to build the container */
node('appserver')
{
    def app
    stage('Cloning Git')
    {
/* This clones the GitHub repository to the Jenkins-workspace folder on the app server */
    checkout scm
    }
    stage('Build-and-Tag')
    {
/* This builds the actual image; 
 * This is synonymous to docker build on the command line */
        app =docker.build("leightoncole/game_docker_repo")
    }
    stage('Post-to-dockerhub')
    {
/* This posts the new image to my DockerHub account */
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
        {
         app.push("latest")
        }
    }
/* This shuts down any running instances and then starts up a new container with the latest image */
    stage('Pull-image-server')
    {
        sh "docker-compose down"
        sh "docker-compose up -d"
    }

}
