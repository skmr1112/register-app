pipeline {
    agent {label 'Jenkins-Agent'}

    tools {
        java 'Java17'
        maven 'Maven394'
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

    
    }
}
