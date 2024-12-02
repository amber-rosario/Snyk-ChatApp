node('ubuntu-AppServer-2140-newest')
{
def app
stage('Cloning Git')
{
   /* Let's make sure we have the repository cloned to our workspace */
   checkout scm
}

stage('SCA-SAST-SNYK-TEST') 
{
  echo 'SCA-SAST-SNYK-TEST'
}

stage('Build-and-Tag')
{
    /* This builds the actual image; 
         * This is synonymous to docker build on the command line */
    app = docker.build('ambrsrio0812/snykchatapp')
}

stage('Post-to-dockerhub')
{
    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
    {
        app.push('latest')
    }
   
}

stage('Deploy')
{
    sh "docker-compose down"
    sh "docker-compose up -d"
}

}
