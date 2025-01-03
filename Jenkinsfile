pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/RamithaHeshan33/GitHub-Action'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t ramitha3333/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'samin-docker', variable: 'samindocker')]) {
                    script {
                        bat "docker login -u ramitha3333 -p %samindocker%"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push ramitha3333/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
