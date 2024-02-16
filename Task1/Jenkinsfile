pipeline{
    agent any
    stages{
        stage('Clean Up'){
          steps{
              sh "echo 'Cleaning Up'"
              sh 'docker rm -f $(docker ps -aq) || true'
              sh "docker network create flasknetwork || true"
          }
          }
        stage('Build Flask App'){
          steps {
              sh "docker build -t flask-app ."
              sh "docker build -t nginx1 -f Dockerfile.nginx ."
          }
        }
          stage('Run Flask App'){
           steps {
               sh "docker run --name -d flask-app --network flasknetwork flask-app"
               sh "docker run --name nginx -d -p 80:80 -f Dockerfile.nginx --network flasknetwork nginx1"
           }
          }
        }  
    }
