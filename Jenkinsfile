pipeline {
  agent any 
    stages {
      stage("Docker Build") {
        steps {
          script {
            last_started = env.STAGE_NAME
          sh "docker build -t docker ."   
          }  
        }
      }
    
     stage("Execute Docker image") {
        steps {
          script {
            last_started = env.STAGE_NAME
          sh "docker run --name nginx -itd -p 8082:80 docker:latest"   
          }  
        }  
      }
      stage("Pushing to docker hub") {
        steps {
          script {
            last_started = env.STAGE_NAME
            //withCredentials([usernamePassword(credentialsId: 'dockerID', passwordVariable: 'pass', usernameVariable: 'userId')]) {
            sh 'docker login -u ${userId} -p ${pass}'
            sh "docker commit nginx vijayvj3/docker:latest"
            sh "docker push vijayvj3/docker:latest"   
            }
          } 
        }
      }     
    }
 /* post {
    success {
    echo 'Successfully completed '    
    }
    failure {
    echo "Build failed at $last_started"
    }  */
  }
}

