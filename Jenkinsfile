pipeline {
     environment {
       IMAGE_NAME = "studentlist_api"
       IMAGE_TAG = "v1"
       STAGING = "walfare-staging"
       PRODUCTION = "walfare-production"
     }
     agent none
     stages {
         stage('Build image') {
             agent any
             steps {
                script {
                  sh 'docker build -t walfare/$IMAGE_NAME:$IMAGE_TAG .'
                }
             }
        }
     stage('Run container based on builded image') {
            agent any
            steps {
               script {
                 sh '''
                    docker run --name $IMAGE_NAME -d -p 81:5000 -e PORT=5000 walfare/$IMAGE_NAME:$IMAGE_TAG
                    sleep 5
                 '''
               }
            }
       }
     stage('Clean Container') {
          agent any
          steps {
             script {
               sh '''
                 docker stop $IMAGE_NAME
                 docker rm $IMAGE_NAME
               '''
             }
          }
     }
    }
}
