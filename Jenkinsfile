pipeline{
    
    agent any;
    stages{
        stage("Code clone/pull"){
            steps{
                git url:"https://github.com/GurmehardeepSingh/Devops_practice.git",branch:"main"
                echo"Code cloned"
            }
        }
        stage("Build"){
            steps{
                sh"docker build -t two-tier-flask-app ."
                echo"Build done"
            }
            
        }
        stage("Test"){
            steps{
            echo"Testing will be done by tester"
            }
        }
        stage("Push to docker-hub")
        {
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHubCred",
                passwordVariable: "dockerHubPass",
                usernameVariable: "dockerHubUser"
                )]){
                sh"docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh"docker tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"
                sh"docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                }
                    
                }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d"
            echo"deployed with docker compose"
            }
        }
    }
    
}
