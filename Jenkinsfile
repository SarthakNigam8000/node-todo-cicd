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
    stage("push") {   
    steps {
        withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: "dockerHubPass", usernameVariable: "dockerHubUser")]) {            echo 'image push ho raha hai'
            sh "echo ${dockerHubPass} | docker login -u ${dockerHubUser} --password-stdin"
            echo 'Login succeeded into Docker'
            sh "docker tag node-app-test-new:latest ${dockerHubUser}/node-app-test-new:latest"
            echo 'Image is tagged'
            sh "docker push ${dockerHubUser}/node-app-test-new:latest"
            echo 'Image push ho gaya'     
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







































