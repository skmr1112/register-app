pipeline {
    agent {label 'Jenkins-Agent'}

    tools {
        jdk 'Java'
        maven 'Maven'
    }
    stages {
        stage('Clean Workspace '){
            steps {
                cleanWs()
            }
        }
        stage('checkout form SCM'){
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/skmr1112/register-app.git'
            }
        }
        stage('Build with maven'){
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('test application'){
            steps {
                sh 'mvn test'
            }
        }
       stage('SonarQube Analysis'){
           steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonarqube-jenkins') {
                        sh "mvn sonar:sonar"
               }
             }
          }
        } 

       stage('Quality gate'){
           steps {
               script {
                   waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube-jenkins'
          }
        }
    }

    
    }
}
