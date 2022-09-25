pipeline {
   agent any
   tools {
     maven "Maven3"  
   }
   environment {
        scannerHome = tool "sonar_scanner"
               //This can be nexus 3 or Nexus 2
        NEXUS_VERSION= "nexus3"
        //This can be http or https
        NEXUS_PROTOCOL= "http"
        //Where your Nexus is running
        NEXUS_URL= "192.168.56.105:8081"
        // Repository Name where we will upload the artifacts
        NEXUS_REPOSITORY= "devops-mvn-repo"
        // Jenkins credentials id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID= "nexus3-credential"
   }

   stages {
      stage('Git Checkout') {
         steps {
            git 'https://github.com/srikanta1219/devops-cicd-workflow.git'   
         }
      }
    stage ('Maven Goal'){
      steps {
         sh "mvn clean install package" 
      }    
    }
        stage('Static code Analisys'){
      steps {
            withSonarQubeEnv('SonarQube') {
            /*sh "${scannerHome}/bin/sonar-scanner -Dsonar.sourceEncoding=UTF-8 -Dsonar.projectKey=testpipeline -Dsonar.projectName=testpipeline -Dsonar.projectVersion=1.0"*/
              sh "mvn sonar:sonar"
             /* sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.0.2:sonar'8*/
        }
      }    
        
    }
    stage ('Deploying Artifact'){
      steps {
        sh "mvn deploy"
       }
     }
   }
   }
