
node {

   stage('Clone Repository') {
        // Get some code from a GitHub repository
        git 'https://github.com/denisdbell/spring-petclinic.git'
    
   }
   stage('Build Maven Image') {
        docker.build("maven-build")
   }
   
   stage('Run Maven Container') {
       
        //Remove maven-build-container if it exisits
        sh " docker rm -u root -f maven-build-container"
        
        //Run maven image
        sh "docker run -u root --rm --name maven-build-container maven-build"
   }
   
   stage('Deploy Spring Boot Application') {
        
         //Remove maven-build-container if it exisits
        sh " docker rm -u root -f java-deploy-container"
       
        sh "docker run -u root --name java-deploy-container --volumes-from maven-build-container -d -p 8080:8080 denisdbell/petclinic-deploy"
   }

}
