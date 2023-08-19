pipeline {
    agent {label 'build'}
   
    stages{
        stage("pull the scm"){
            steps{
                git 'https://github.com/shubhlze/two-tier-flask-app.git'
            }
        }
        stage("build"){
            steps{
                sh 'docker build -t to-do .'
        withCredentials([usernamePassword(credentialsId: 'dockerhub1', passwordVariable: 'password', usernameVariable: 'dockerhub')]) {
    // some block
                sh 'docker login -u ${dockerhub} -p ${password}'
                sh 'docker tag to-do shubhlze/to-do:latest'
                sh 'docker push shubhlze/to-do:latest'
        
}
                
            }
        }
        stage("test"){
            steps{
                echo "test"
            }
        }
        stage("deploy"){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
