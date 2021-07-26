pipeline {
   agent any
        environment{
    mavenHome = tool 'Maven'
        scannerHome = tool 'SonarQube'
        }
    stages{
        /* stage('git Checkout'){
            steps{
                git credentialsId: 'git_creds', url: 'git_url'
   
                 }
    } */
    stage('Build'){
        steps{
            sh 'mvn clean package'
        }
    }
   
    stage('Sonar-scan'){
        steps{
        withSonarQubeEnv('rigSonarQubeServer'){
             sh "${scannerHome}/bin/sonar-scanner -Dproject.settings=./sonar-project.properties"
        }
        }
    }
   
    stage('Quality Gate'){
         steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
    }
    }
}