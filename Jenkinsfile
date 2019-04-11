node {
   
    
        stage("checkout"){
            
                git credentialsId: '3fb46b3b-b800-453f-9bc2-2d15b01dbb4e', url: 'https://github.com/pavants52/CR-OnBoarding'
            
        }

        stage("static code analysis"){
            
                withSonarQubeEnv('SonarQube') {
                    sh '/opt/sonar/bin/sonar-scanner -Dsonar.projectKey=pavants52_CR-OnBoarding -Dsonar.sources=api'
                }
            
        }

        stage("build docker image"){
            
                sh "docker-compose build"
            
        }


        stage("env cleanup"){
            
                sh "docker image prune -f"
            
        }

        stage("Launch service"){
            
                sh "docker-compose stop"
                sh "docker-compose up -d"
            
        }

        stage("Launch Info"){
            
                echo "service running on ${ip}"
            }
        

    }


