pipeline{
    agent{
        label "slave1"
    }
    tools{
        jdk 'Java17'
        nodejs 'node16'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/abhigyanbasu/netflx.git'
            }
        }
        
        
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker'){   
                       sh "docker build --build-arg TMDB_V3_API_KEY=116bd67098c7720fa45f789d76d32c7d -t netflix ."
                       sh "docker tag netflix abhigyanbasu/netflix:latest "
                       sh "docker push abhigyanbasu/netflix:latest "
                    }
                }
            }
        }
    }
}