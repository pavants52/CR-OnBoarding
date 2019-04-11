node {
   
    
        stage("checkout"){
            
                git credentialsId: '3fb46b3b-b800-453f-9bc2-2d15b01dbb4e', url: 'https://github.com/pavants52/CR-OnBoarding'
            
        }

        stage("static code analysis"){
            
                withMaven(jdk: 'java8 ', maven: 'maven 3.6.0') {
          sh 'mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent package sonar:sonar ' +
          ' -Dsonar.host.url=https://sonarcloud.io '+
          ' -Dsonar.organization=pavants52-github ' +
         ' -Dsonar.login=6dd85dc7820c0b59f3cd2e15b71d3a5437045b40 '                 }
            
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


