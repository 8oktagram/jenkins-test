pipeline {
    agent {
        docker {
            image 'node:16-buster-slim' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install'
            }
        }
        stage('Test') { 
            steps {
                sh "chmod +x -R ${env.WORKSPACE}"
                sh './jenkins/scripts/test.sh' 
            }
        }  
        stage('Deploy'){
            steps{
                sh'./jenkins/scripts/deliver.sh'
                input massage: 'Jika sudah berhasil menjalankan klik ("Procced") untuk mengakhiri'
                sh'./jenkins/scripts/kill.sh'
            }
        }  
    }
}