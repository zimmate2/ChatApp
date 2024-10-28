node('ubuntu-APPserver')
{

def app 
stage('Cloning git')
{
    /*code for cloning repository to our workspace */
    checkout scm
}
stage('SCA-SAST-SNYK-TEST')
    {
      agent
      {
        label 'ubuntu-APPserver'
      }
      steps
      {
        snykSecurity(
            snykInstallation: 'Synk',
            snykTokenId: 'snykid',
            severity: 'critical'
        )
      }
    }
 
stage('Build-and-tag')
{
    /*this builds the image
        this is synonymous to docker build on the CLI */
    app = docker.build('zimmate222/chatapp')
}

stage('Push-to-dockerhub')
{
    /* this code pushes the changes to docker hub*/
    docker.withRegistry('https://registry.hub.docker.com', 'zimmate')
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
