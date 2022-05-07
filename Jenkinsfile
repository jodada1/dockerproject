pipeline { 
     environment { 
         registry = "jodada1/new-apache" 
         registryCredential = 'dockerhub'
         dockerImage = '' 
     }
     agent any 
     stages { 
         stage('Cloning our Git') { 
             steps { 
                 git 'https://github.com/jodada1/dockerproject.git' 
             }
         } 
         stage('Building image Docker') { 
             steps { 
                 script { 
                     dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                 }
             } 
         }
         stage('Deploy our image to Dockerhub') { 
             steps { 
                 script { 
                     docker.withRegistry( '', registryCredential ) { 
                         dockerImage.push()
                         dockerImage.push('latest') 
                     }
                 }
             }
         } 
     }
 }       