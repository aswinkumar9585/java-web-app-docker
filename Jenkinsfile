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
     
      
