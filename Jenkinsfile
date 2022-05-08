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
         stage('Building latest Docker image') { 
             steps { 
                 script { 
                     dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                 }
             } 
         }
         stage('Deploy image to Dockerhub') { 
             steps { 
                 script { 
                     docker.withRegistry( '', registryCredential ) { 
                         dockerImage.push()
                         dockerImage.push('latest') 
                     }
                 }
             }
         }    
