pipeline {
    agent any 
    
    stages{
        stage("code"){
            steps{
                git url: "https://github.com/Kajalchhetri/ci_cd_project.git", branch: "master"
                
            }    
            
        }
        stage("Build"){
            steps{
                sh "docker build . -t node-app-demo"
            }    
            
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker tag node-app-demo:latest ${env.dockerHubUser}/node-app-demo:latest"
                    sh "docker push ${env.dockerHubUser}/node-app-demo:latest"
                    echo "code push hogaya"
                    
                    
                }
                
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo "code is deployed"
            }    
            
        }
    }
}
