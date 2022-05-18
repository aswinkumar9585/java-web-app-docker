node{
     
    stage('SCM Checkout'){
        git url: 'https://github.com/aswinkumar9585/java-web-app-docker.git',branch: 'master'
    }
    
    stage(" Maven Clean Package"){
      def mavenHome =  tool name: "Maven", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
      
    } 
    
    
    stage('Build Docker Image'){
        sh 'docker build -t aswin6493/java-web-app .'
    }
    
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker_Hub_Pwd')]) {
          sh "docker login -u aswin6493 -p ${Docker_Hub_Pwd}"
        }
        sh 'docker push aswin6493/java-web-app'
     }
     stage('Run Docker Image In Dev Server'){
        
        def dockerRun = ' docker run  -d -p 8080:8080 --name java-web-app aswin6493/java-web-app'
         
         sshagent(['DOCKER_SERVER']) {
          sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.86.80.182 docker stop java-web-app || true'
          sh 'ssh  ubuntu@3.86.80.182 docker rm java-web-app || true'
          sh 'ssh  ubuntu@3.86.80.182 docker rmi -f  $(docker images -q) || true'
          sh "ssh  ubuntu@3.86.80.182 ${dockerRun}"
       }
       
    }
     
     
}
      

