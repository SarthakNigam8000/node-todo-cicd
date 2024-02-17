pipeline {
    agent any 
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/SarthakNigam8000/node-todo-cicd.git", branch: "master"
           
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t node-app-test-new ."

            }
        }
        stage("scan image"){
            steps{
                echo 'image scanning ho gayi'
            }
        }
       stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                echo 'image push ho raha hai'
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app-test-new:latest ${env.dockerHubUser}/node-app-test-new:latest"
                sh "docker push ${env.dockerHubUser}/node-app-test-new:latest"
                echo 'image push ho gaya'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
    
            }
        }
    }
}
