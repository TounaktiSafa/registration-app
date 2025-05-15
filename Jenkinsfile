pipeline {
    agent any
   tools {
     jdk 'Java17' 
     maven 'Maven3'
   }

    stages {
        stage('Cleanup Workspace') {
            steps {
              cleanWs()  
              
            }
        }
      stage('Checkout from SCM'){
        steps {
          git branch: 'main', credentialsId: 'github' , url:'https://github.com/TounaktiSafa/registration-app'
        }
      }

      stage('Build Application') {
          steps {
            sh "mvn clean package"
          }            
      }
      stage ('Test') {
        steps {
          sh 'mvn test'
        }
      }
    stage('SonarQube Analysis'){
        steps {
            script {
                withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token'){
                    sh "mvn sonar:sonar"
                }
            }
  
            
        }
    }
 }
}
