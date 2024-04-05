pipeline{
    agent {label 'dev-agent'}
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/sowmya-bm/node-todo-cicd.git', branch: 'master'
                }
            
        }
        stage('Build'){
            steps{
                sh "docker build -t sowmyabm/node-todo-cicd ."
              
            }
        }
        stage('Login and push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'sowmya-bm', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUsername')]) {
                sh "docker login -u ${env.dockerHubUsername} -p ${env.dockerHubPassword}"
                sh "docker push sowmyabm/node-todo-cicd:latest"
                
                }
            }    
        }
        stage('Test'){
            steps{
                echo "Tested"
            }
            
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo "Deployed"
                
            }
            
            
        }
    }
}
