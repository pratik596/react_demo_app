pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/pratik596/react_demo_app.git", branch: "master"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t react-app-test-new"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker tag node-app-test-new ${env.dockerHubUser}/react-app-test-new:latest"
                    sh "docker push ${env.dockerHubUser}/react-app-test-new:latest" 
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
