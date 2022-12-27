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
                
                sh "docker build -t 9100246253/img01"
            }
        }
        stage('Docker Push') {
            steps {
                sh "docker login -u peetla-p xxxxxxx"
                sh "docker push peetla/hiring:0.0.2"
            }
        } 
    }
}
