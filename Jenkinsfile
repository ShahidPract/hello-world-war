pipeline {
  agent { label 'master' }
    stages {
    stage('checkout') {
      steps {
        sh 'sudo rm -rf hello-world-war'       
        sh 'git clone https://github.com/ShahidPract/hello-world-war.git'
        }
    }
   
    stage('build') {
      steps {
	sh 'sudo chmod 777 /var/run/docker.sock'	
	sh 'docker build -t myimage:latest .'
        }
    }
   
   stage('login') {
     steps {
            sh 'docker login -u sanadishahid -p Shah@7091'
            sh 'docker tag myimage:latest sanadishahid/multistage1:1.0'
            sh 'docker push sanadishahid/multistage1:1.0'
      }
   }
	    
   stage('deploy') {
	   agent { label 'tomcat' }
     steps {
       	    sh 'docker login -u sanadishahid -p Shah@7091'
            sh 'docker pull sanadishahid/multistage1:1.0'
            sh 'docker rm -f test1'
	    sh 'docker run -d -p 8054:8080 --name test1 sanadishahid/multistage1:1.0'
     }
   }
   }
}
