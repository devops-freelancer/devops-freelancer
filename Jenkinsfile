pipeline {
            agent any
tools       {    
                  'maven'

       }
environment {

ArtifactId =  readMavenPom().artifactId()
Version    =  readMavenPom().getversion()
Name       =  readMavenPom().getname()
GroupId    =  readMavenPom().getgroupid()

}
   stages {



stage('Checkout') {

                           steps  {
                                   checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: '<GIT_REPO_URL>']]])
                                  }

                                 }

stage ("Build") {
steps   {  

           echo "Building..."
sh 'maven clean install package'
}

  stage ("Test") {
      steps   {   echo "Testing..."

                       }
              
 stage ("Publish to Nexus") {
    steps {      
               echo "Publishing to Nexus..."
               nexusArtifactUploader artifacts: [[artifactId: '${ArtifactId}',
                    classifier: '',
                    file: 'target/com.freelancer.app-snapshot-1.0.war',
                    type: 'war']],
                    credentialsId: '',
                    groupId: ' ${GroupId}',
                    nexusUrl: '192.168.1.5:8086',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'com.freelancer.app-snapshot-1.0',
                   version: '${Version}'
               }

stage ("Printing environment variable.....") {
                 

steps {     echo "ArtifactId is : ${ArtifactId}
            echo "Version is    : ${Version}
            echo "Name  is      : ${Name}
            echo "GroupId  is   : ${GroupId}
}
                        }

stage ("Deploy") {
                 

steps {     echo "Deploying..."

}

               
}

}
