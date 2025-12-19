pipeline{
    
    agent any;
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/Shubham-Aswekar/flask-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps{
               sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("Test"){
            steps{
                echo "Developer/tester test likh ke dega"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(
                credentialsId: "DockerHubCreds",
                passwordVariable: "dockerHubPass",
                usernameVariable: "dockerHubUser"
            )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag flask-app ${env.dockerHubUser}/flask-app"
                sh "docker push ${env.dockerHubUser}/flask-app:latest"
            }

            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
        
    }
    
}
