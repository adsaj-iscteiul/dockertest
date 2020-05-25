def dockeruser = "adsaj"
def imagename = "ubuntu:16"
def container = "apache2"
node {
   echo 'Building Apache Docker Image'

stage('Git Checkout') {
    git 'https://github.com/adsaj-iscteiul/dockertest.git'
    }
    
stage('Build Docker Image'){
     sh "docker build -t  ${imagename} ."
    }
    
stage('Stop Existing Container'){
     sh "docker stop ${container}"
    }
    
stage('Remove Existing Container'){
     sh "docker rm ${container}"
    }
    
stage ('Running Container to test built Docker Image'){
    sh "docker run -dit --name ${container} -p 80:80 ${imagename}"
    }
    
stage('Tag Docker Image'){
    sh "docker tag ${imagename} ${env.dockeruser}/ubuntu:16.04"
    }

stage('Docker Login and Push Image'){
    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'dockerpasswd', usernameVariable: 'dockeruser')]) {
    sh "docker login -u ${dockeruser} -p ${dockerpasswd}"
    }
    sh "docker push ${dockeruser}/ubuntu:16.04"
    }

}
