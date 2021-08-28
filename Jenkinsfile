node {    
      def app     
      stage('Clone repository') {               
             
            checkout scm    
      }     
      stage('Build image') {         
       
            app = docker.build("pranav744/test")    
       }     
      stage('Test image') {           
            app.inside {            
             
             sh 'echo "Tests passed"'        
            }    
        }     
       stage('Push image') {
                                                  docker.withRegistry('https://registry.hub.docker.com', 'git') {            
       app.push("${env.BUILD_NUMBER}")            
       app.push("latest")        
              }    
           }
       stage('Deploy') {
         def dockerRun = 'docker run -p 85:80 -d --name project pranav744/test'
         sshagent(['prod-server']) {
               sh "ssh =o StrictHostKeyChecking=no root@172.31.33.246 ${dockerRun}"
         }
    
        }
}
