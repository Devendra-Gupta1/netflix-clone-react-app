pipeline{
    agent { label 'dev' }
    stages{
        stage ("cloning code"){
        steps{
            echo"code pulling from Git hub"
            git url: 'https://github.com/Devendra-Gupta1/netflix-clone-react-app.git' , branch: 'main'
        }
        }
        
        stage("build the images"){
        steps{
            echo "building the image"
            sh "docker build -t  netflix-clone-react:latest ."
        }
        }
        
        stage("login & pusing the images"){
        steps{
            echo "login & pusing the images on docker_hub"
            withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                
            sh "docker tag netflix-clone-react ${env.dockerHubUser}/netflix-clone-react:latest"
            
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
            
            sh "docker push ${env.dockerHubUser}/netflix-clone-react:latest"
            }
        }
        }
        
        stage ("deploy"){
        steps{
            echo"deploying the code in conatiner"
            sh "docker run -t --name=netflix-project -p 80:80  devendrag12/netflix-clone-react:latest"
        }
        }
        }
        
    }
