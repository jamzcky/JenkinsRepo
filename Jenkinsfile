node {
   def mvnHome
   stage('RepoClone') { // for display purposes
      // Get some code from a GitHub repository
      git credentialsId: 'dd428ca3-5959-4a8a-a0fc-20ede432d526', url: 'https://github.com/jamzcky/DevOpsCaseStudy_G3.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
           // bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            echo 'maven clean'
                //ABC indicates the folder name where the pom.xml file resides
                bat ' mvn -f CalculatorDivision/pom.xml clean package'  
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts '**/target/*.jar'
   }
   
   
   /*
Go to the project/workspace named "Create_archive".
Look in the folder "packages" for the file(s) "target*.zip".
Copy that file(s) into the folder "Archive", in the local workspace.  Folder will be created if it doesn't already exist.
   
   stages {
     stage('Copy Archive') {
         steps {
             script {
                 step ([$class: 'CopyArtifact',
                 projectName: 'CalculatorDivision',
                 filter: "**/target/*.zip",
                 target: 'Archive']);
             }
         }
     }
   }*/
}
