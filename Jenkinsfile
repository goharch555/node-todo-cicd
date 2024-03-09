pipeline {
    agent { label "dev-server"}
    stages {
        stage("Code"){
            steps{
                git url: "https://github.com/goharch555/node-todo-cicd.git", branch: "master"
                echo 'code build ho gaya' 
            }
        }
         stage("Build and Test"){
            steps{
               sh "docker build -t node-app ."
                echo 'code build bhi ho gaya'
            }
        }
         stage("Push To DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub1",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app:latest ${env.dockerHubUser}/node-app:latest"
                sh "docker push ${env.dockerHubUser}/node-app:latest"
                echo 'code push ho gaya'
                }
            }
        }
         stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'deployment ho gai'
            }
        }
    }
}
