
node {
   stage('Git Clone') { 
      // Get some code from a GitHub repository
      git 'https://github.com/walidsaad/maven-jenkins-pipeline.git'
   }
        
   stage('Build Docker Maven Image') {
      // Run the maven docker build
   echo "Build Docker Maven Image With Sample WebApp"
   sh "docker build -t=\"mymaven:v2.0\" ./maven/"
   }
   stage('Generate Maven Artifact') {
   echo "Run Docker Container and Generate Artifcat"
   sh "docker run --rm -d -v /home/stagiaire/.m2:/root/.m2 -w /app/training-webapp/ --name test-maven  mymaven:v2.0 mvn clean install"
   
   }
    stage('Deploy Artifcat') {
      // Run the tomcat deploy
   echo "Build Tomcat Image with Artifact"
   sh "docker build -t=\"mytomcat:v2.0\" ./tomcat/"
   echo "Run Tomcat Container"
   sh "docker run --rm -d -v /home/stagiaire/.m2/repository/com/mycompany/app/training-webapp/1.0-SNAPSHOT/:/usr/local/tomcat/webapps/ -p 8888:8080 --name maven-webapp mytomcat:v2.0"
   }

}
