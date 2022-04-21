pipeline {
agent {label 'tomcat'}
stages{
stage('checkout'){
steps{
sh 'git pull https://github.com/Urssharath/hello-world-war.git'
}
}
stage('build'){
steps{
sh 'mvn clean package'
}

}
stage('deploy'){
steps{
sh 'echo "giving sudo permission for jenkins folder"'
sh 'sudo chmod -R 0777 /opt'
sh 'cp -R /home/jenkins/workspace/ppjava/target/hello-world-war-1.0.0 /opt/apache-tomcat-9.0.56/webapps'
}
}
}
}
