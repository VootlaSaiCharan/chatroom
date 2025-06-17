pipeline{
    agent any
    tools{
        maven 'maven-3.9.10'
    } 
    stages{
        stage('clone'){
            steps{
                git 'https://github.com/VootlaSaiCharan/chatroom.git'
            }
        }
        stage('validate'){
            steps{
                sh 'mvn --version'
                sh 'mvn clean validate'
            }
        }
        stage('compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('package'){
            steps{
                sh 'mvn package'
            }
        }
    }
}