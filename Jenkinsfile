pipeline {
  environment {
        DOCKERHUB_CREDENTIALS=credentials('haleema-dockerhub')
    }
  agent none
  stages {
    stage('data transfer b/w rpi & edge') {
      parallel {
        stage('On-Edge1') {
          agent any
          steps {
            sh 'echo "edge1"'
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-edge1.git'
            //sh 'docker build -t haleema/docker-edge1:latest .'
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-edge1'

          }
        }
          stage('On-RPI') {
          agent {label 'linuxslave1'}
          steps {
            sh 'echo "rpi" '
            git branch: 'main', url: 'https://github.com/HaleemaEssa/first_jenkins_project.git'
           // sh 'docker build -t haleema/docker-rpi:latest .'
             sh 'docker run --privileged -t haleema/docker-rpi'
          }
        }
}
}
}





	}//pipe
