pipeline
{
    
    agent any
     
    stages
    {
        stage("Code")
        {
            steps
            {
                git url:"https://github.com/bhargavpatel199316/two-tier-flask-app.git", branch: "master"
            }
        }
        stage("Build and Test") 
        {
            steps
            {
            sh "docker build . -t two-tier-flask-app" 
                
            }
            
        }
        
        stage("Docker Login")
        { steps{
            withCredentials([usernamePassword(credentialsId: 'dockerhub' , usernameVariable: 'dockerUser' , passwordVariable: 'dockerPass' )])
                {
                    sh "docker login -u ${env.dockerUser} -p ${env.dockerPass}"
                    sh "docker tag two-tier-flask-app ${env.dockerUser}/two-tier-flask-app:latest"
                    sh "docker push ${env.dockerUser}/two-tier-flask-app:latest"
                }
          }  
        }
        stage("deploy")
        {
            steps{
                sh " docker-compose down && docker-compose up -d"
            }
        }
    }
    
}
