pipeline {
  agent any // means run on any machine that is available to Jenkins
  tools {
        maven "M3"
   }
  // this is a dummy change
  stages {



     stage('Build Artifact')
      {
            steps
            {
             //git remote prune https://github.com/alirezanoori021/maven-jenkins/
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar'
            }  
       }
      stage('Test Maven - JUnit')
      {
            steps
            {
              //sh "mvn test"
              mvn clean verify sonar:sonar \
              -Dsonar.projectKey=maven-jenkins-pipelines \
              -Dsonar.host.url=http://35.242.132.146:9000 \
              -Dsonar.login=sqp_2b0930ac35906edec16648b09bc2e8280b094b26
              echo "Running unit tests"
            }
      }
    stage('Sonarqube Analysis - SAST')  
      {
        steps  
        {
           withSonarQubeEnv('SonarQube')  
           {
              sh "mvn sonar:sonar -Dsonar.projectKey=maven-jenkins-pipeline -Dsonar.host.url=http://35.242.132.146:9000/"  
           }
        }
      }
    
    
    
      stage('Dev Environment')
      {
          steps
          {
              echo "I'm now deploying to the dev environment"
          }
      }
      stage('Test Environment')
      {
          steps
          {
              echo "I'm now deploying to the test or QA environment"
          }
      }
      stage('UAT Environment')
      {
          steps
          {
              input('Continue to Deploy?')
              echo 'Deploying to Production Environment'
          }
      }
      stage('Production Environment')
      {
          steps
          {
              input('Continue to Deploy?')
              echo 'Deploying to Production Environment'
          }
      }
    }
}
