pipeline {
  agent {label 'master'}
  stages {
    stage ('checkout') {
      steps {
              sh 'whoami'
              sh 'rm -rf hello-world-war'
              sh 'git clone https://github.com/ShahidPract/hello-world-war.git'
              sh 'pwd'
              sh 'ls'
      }
    }
    stage ('build') {
      steps {
              sh 'docker build -t 963946019663.dkr.ecr.us-east-1.amazonaws.com/tomcat:${BUILD_NUMBER} .'
      }
    }
    stage ('publish') {
      steps {               
              sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 963946019663.dkr.ecr.us-east-1.amazonaws.com'
              sh 'docker push 963946019663.dkr.ecr.us-east-1.amazonaws.com/tomcat:${BUILD_NUMBER}'
              sh 'pwd'
              sh 'ls'
              sh "helm package --version ${BUILD_NUMBER} helm/tomcat/ "
              sh "curl -ushahidasanadi123@gmail.com:Shah@7091 -T tomcat-${BUILD_NUMBER}.tgz \"https://shahjfrog.jfrog.io/artifactory/tomcat-helm/tomcat-${BUILD_NUMBER}.tgz\""
      }
    }
      
    stage ('deploy') {
      agent {label 'slavecicd'}
      steps {
              sh "helm repo add tomcat-helm https://shahjfrog.jfrog.io/artifactory/api/helm/tomcat-helm --username shahidasanadi123@gmail.com --password Shah@7091"
              sh "helm repo update"
              sh "helm upgrade --install tomcat tomcat-helm/tomcat --set image_tag=${BUILD_NUMBER} --version ${BUILD_NUMBER}"
      }
    }
  }         
}
