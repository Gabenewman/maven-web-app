//Jenkins pipeline script
//Groovy script 

node{
  def mavenHome = tool name: 'maven3.8.1'
  stage('CodeClone') {
    git credentialsId: 'git-credentials', url: 'https://github.com/mylandmarktechs/web'
  }
  stage('mavenBuild') {
    sh "${mavenHome}/bin/mvn clean package"
  }

  stage('CodeQuality') {
    sh "${mavenHome}/bin/mvn sonar:sonar"
  // execute the CodeQuality report with sonar
  }

   stage('UploadNexus') {
    //sh "${mavenHome}/bin/mvn deploy"
    //mvn deploy  are uploaded in to nexus
  }

  stage('DeployDocker') {
    
    sh "docker build -t image3 ."
    sh "docker run -d -p 6000:8080 image3"

  stage('emailDeployIssues') {
    emailext body: '''Thanks

Landmark Technologies''', recipientProviders: [developers()], subject: 'status of build', to: 'mylandmarktech@gmail.com'
  }
}
