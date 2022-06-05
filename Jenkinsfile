pipeline {
  agent {label 'newslave'}
  stages {
    stage ('checkout') {
      steps {
              sh 'whoami'
              sh 'rm -rf hello-world-war'
              sh 'git clone https://github.com/venuumarji/hello-world-war.git'
              sh 'pwd'
              sh 'ls'
      }
    }
    stage ('build') {
      steps {
              sh 'docker build -t 377663637476.dkr.ecr.us-east-1.amazonaws.com/mytomcat:${BUILD_NUMBER} .'
      }
    }
    stage ('publish') {
      steps {               
              sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 377663637476.dkr.ecr.us-east-1.amazonaws.com'
              sh 'docker push 377663637476.dkr.ecr.us-east-1.amazonaws.com/mytomcat:${BUILD_NUMBER}'
              sh 'pwd'
              sh 'ls'
              sh "helm package --version ${BUILD_NUMBER} helm/mytomcat/ "
              sh "curl -uvenu.umarji@gmail.com:Jfrog@123 -T mytomcat-${BUILD_NUMBER}.tgz \"https://venu.jfrog.io/artifactory/mytomcat-helm/mytomcat-${BUILD_NUMBER}.tgz\""
      }
    }
      
    stage ('deploy') {
      agent {label 'eksslave'}
      steps {
              sh "helm repo add mytomcat-helm https://venu.jfrog.io/artifactory/api/helm/mytomcat-helm --username venu.umarji@gmail.com --password Jfrog@123"
              sh "helm repo update"
              sh "helm upgrade --install tomcat mytomcat-helm/mytomcat --set image_tag=${BUILD_NUMBER} --version ${BUILD_NUMBER}"
      }
    }
  }         
}
