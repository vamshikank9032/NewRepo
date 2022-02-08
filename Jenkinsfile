pipeline {
    agent none
    tools { 
        maven "maven-3.8"
        
    }
    stages {
        stage("build and test the project") {
            agent {
                label 'BuildServer'
            }
            stages {
               stage("build") {
                   steps {
                       sh "echo hel"
                   }
               }
               stage("checkout") {
                   steps {
                    checkout([$class: 'GitSCM', branches: [[name: '*/dev']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vamshikank9032/NewRepo.git']]])

                   }
               } 
               stage("show") {
                   steps {
                     sh "ls"

                   }
               } 
               stage("Build") {   
				   steps {
                       sh "mvn clean install"
			       }
			   }  
              
              stage("copy") {
                   steps {
                       sh 'sudo cp -r /home/centos/jenkins/workspace/testpiipeline2/mywebapp/src/main/webapp/ /home/centos/opt/tomcat/webapps/'
                   }
               }	
              stage("approval") {
                   steps {
                      echo 'Approval'
                      timeout(time: 2, unit: 'HOURS') {
                      input message: 'Do you want to move',submitter:'kvk'
	                                               	}
		                 }
		                        }
            }
              post {
                success {
                   sh "echo Sending to Production"
                }
            }
        }

        stage("deploy the artifacts if a user confirms") {
            agent {
                label 'ProdServer'
            }
            stages {
               stage("build") {
                   steps {
                       sh "echo hel"
                   }
               }
               stage("checkout") {
                   steps {
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vamshikank9032/NewRepo.git']]])

                   }
               } 
               stage("show") {
                   steps {
                     sh "ls"

                   }
               } 
               stage("Build") {   
				   steps {
                       sh "mvn clean install"
			       }
			   }  
              
              stage("copy") {
                   steps {
                       sh 'sudo cp -r /home/centos/jenkins/workspace/testpiipeline2/mywebapp/src/main/webapp/ /home/centos/opt/tomcat/webapps/'
                   }
               }	
              
            }
            
        }

        }
    }
