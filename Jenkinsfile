pipeline {
	agent { label 'master' }
   stages {
     stage('checkout') {
       steps {
      	sh 'git clone https://github.com/ShahidPract/hello-world-war.git'
	}
      }
   stage('build') {
        steps {
	  sh 'docker build -t myimage:latest .'
    }
   }
   
   stage('login') {
        steps {
	  sh 'docker login -u sanadishahid -p Shah@7091'
	  sh 'docker tag myimage:latest multistage1:1.0'
	  sh 'docker push sanadishahid/multistage1:1.0'
    }
   }
   }
}
