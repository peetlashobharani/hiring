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
                
                sh "docker build -t peetla/hiring:0.0.2 ."
            }
        }
       stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-creds', passwordVariable: 'pwd', usernameVariable: 'usr')]) {
                      // some block
                    sh "docker log -u peetla -p xxxxx"
                    sh "docker push peetla/hiring:0.0.2"
                }
            }
        }
    }
}
