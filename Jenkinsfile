pipeline{
    
<<<<<<< HEAD
    agent {label "dev"};
=======
    agent { label "dev"};
>>>>>>> 1bbd80e4709941698f762c7d23b3f1c77bf325f8
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/Shubham-Aswekar/flask-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps{
               sh "docker build -t flask-app ."
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
    post{
        success{
            script{
                emailext from: "shubham.aswekar12@gmail.com",
                to: "shubham1styearengg@gmail.com",
                body: "Build Successfull for flask-app",
                subject: "Build Success for flask-app"
            }
        }
        failure{
            script{
                emailext from: "shubham.aswekar12@gmail.com",
                to: "shubham1styearengg@gmail.com",
                body: "Build Failed for flask-app",
                subject: "Build Failed for flask-app"
            }
        }
    }
    
}    
