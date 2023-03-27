pipeline{
    agent any
    
    environment{
        DOCKERHUB_CREDENTIALS = credentials('adeyemi-docker-credentials')
    }
    stages{
        stage('Check out') {
          steps {
            checkout scm
          }
        }
        stage('Build Maven Project') {
          steps {
            sh 'mvn clean package'
          }
        }
        stage("Docker Build"){
            steps{
                sh 'echo "Docker build"'
                sh 'docker build -t theyemi/theyemi-exercise1-docker-image ./'
            }
        }
        stage('Docker Login'){
            steps {
                sh 'echo "Logging into docker"'	
                sh 'docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW'	
            }
        }
        stage('Docker Push'){
            steps {
                sh 'echo "Docker Push"'	
                sh 'docker push theyemi/theyemi-exercise1-docker-image'	
            }
        }
    }
    post{
        always{
            sh 'docker logout'
        }
    }
}
