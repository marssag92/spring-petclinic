
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
        //sh " docker rm -f maven-build-container"
        
        //Run maven image
        sh "docker run --name maven-build-container maven-build"
   }
   
   stage('Deploy Spring Boot Application') {
        
        sh "docker run -i -p 8000:8000 --name java-build-container --volumes-from maven-build-container maven-build:latest"
   }

}
