pipeline {
    agent any

    stages {
        
        stage('Maven Build') {
            
            steps {
                sh "mvn clean package"
            }
        }
        
        stage('Docker Build') {
            steps {
                
                sh "docker build . -t peetla/hiring:${commit_id()}"
            }
        }
       stage('Docker Push') {
            steps {
               
                    sh "docker login -u peetla -p aug@071995 "
                    sh "docker push peetla/hiring:${commit_id()}"
                }
            }
        stage('Docker Deploy') {
            steps {
                sshagent(['docker-host']) {
                    sh "ssh -o StrictHostKeyChecking=no  ec2-user@172.31.38.30 docker rm -f hiring"
                    sh "ssh  ec2-user@172.31.38.30 docker run -d -p 8080:8080 --name hiring peetla/hiring:${commit_id()}"
                }
            }
        }

    }
}
 
def commit_id(){
    id = sh returnStdout: true, script: 'git rev-parse HEAD'
    return id 
}
