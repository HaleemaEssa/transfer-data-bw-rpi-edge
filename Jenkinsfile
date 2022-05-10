pipeline {
  environment {
        DOCKERHUB_CREDENTIALS=credentials('haleema-dockerhub')
    }
  agent none
  stages {
    stage('data transfer b/w rpi & edge') {
      parallel {
        stage('On-Edge1') {
		options {
                timeout(time: 30, unit: "SECONDS")
            }
   
          agent any
        
          steps {
            script { 
            try {
            sh 'echo "edge1"'
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-edge-rec.git'
            //sh 'docker build -t haleema/docker-edge1:latest .'
            echo "Started stage A"
            sleep(time: 3, unit: "SECONDS")
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-edge1'
            sleep(time: 2, unit: "SECONDS")
               } catch (Throwable e) {
                        echo "Caught ${e.toString()}"
                        currentBuild.result = "SUCCESS" 
                        //sh 'nano data.csv'             
                    }
              //if (currentBuild.result == 'SUCCESS') {
               // sh 'sleep 2'
                //sh 'nano data.csv'
                //sh 'exit 0' 
              
              //}
              
            }

          }
        }
		
          stage('On-RPI') {
		   options {
                timeout(time: 40, unit: "SECONDS")
            }
          agent {label 'linuxslave1'}
          steps {
             script { 
            try {
            sh 'echo "rpi" '
            git branch: 'main', url: 'https://github.com/HaleemaEssa/first_jenkins_project.git'
            //sh 'docker build -t haleema/docker-rpi:latest .'
            sleep(time: 3, unit: "SECONDS")
            sh 'docker run --privileged -t haleema/docker-rpi'
            sleep(time: 4, unit: "SECONDS")
               } catch (Throwable e) {
                        echo "Caught ${e.toString()}"
                        currentBuild.result = "SUCCESS" //currentBuild.result = 'SUCCESS'
                    }
          }
        }//parallel
		  
		  
		  
         
}
}
}
	}//pipe
