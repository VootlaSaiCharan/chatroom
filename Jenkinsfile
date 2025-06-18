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
        stage('trivy-file-scan'){
            steps{
                sh 'trivy fs --severity HIGH,CRITICAL --format json --output trivy-fs-result.json .'
                sh ''' trivy convert \
                --format template --template "@/usr/local/share/trivy/templates/html.tpl" \
                -o trivy-fs-result.html trivy-fs-result.json '''
            }
        }
        stage('package'){
            steps{
                sh 'mvn package'
            }
        }
        stage('deploy'){
            steps{
                sh 'cp -r target/chatroom-0.0.1-SNAPSHOT.war /usr/local/tomcat/webapps/ROOT.war'
            }
        }
    }
}