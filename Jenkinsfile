pipeline {
    agent any


    stages {
       
        
        stage('MVN CLEAN') {
            steps {
               
              script {

                  sh 'mvn  clean'

 
                      }
                   }        
         }
          stage('MVN compile') {
            steps {
               
              script {

                  sh 'mvn  compile'

 
                      }
                   }        
         }
          
  	    stage('MVN test') {
            steps {
               
              script {

                  sh 'mvn  test'

 
                      }
                   }  
		  } 
          stage('SONAR') {
            steps {
               
              script {

                  sh 'mvn  sonar:sonar  -Dsonar.sources=src/main/java -Dsonar.css.node=. -Dsonar.java.binaries=. -Dsonar.host.url=http://192.168.118.91:9000/ -Dsonar.login=admin   -Dsonar.password=sonar'

 
                      }
                   }   
                   
         }
         
          stage('Artifact Construction') {
                      steps{
                          sh "mvn -B -DskipTests  package "
                      }
                  }
         stage('nexus') {
            steps {
               
              script {

sh 'mvn  deploy -e'                      }
                   }         
         }
     stage('Build Docker Image'){
            steps {
                script{
				    sh 'docker image build -t obettaieb/backcicd .'
                }    
            }
		}
		stage('Docker login') {
                      steps {
                          script {
                        
                              sh 'docker login -u obettaieb -p Mypwdocker13'}
                      }
                      }
	    /*
                  stage('Pushing Docker Image') {
                      steps {
                          script {
                           
                           sh 'docker push obettaieb/backcicd'
                          }
                      }
                } */
                stage('Run Spring && MySQL Containers') {
                      steps {
                          script {
                            sh 'docker-compose up -d'
                          }
                      }
                  }
	            stage('Sending email'){
           steps {
            mail bcc: '', body: '''Ping.. ,
            Pipeline successfully executed  .
            Keep Up The Good Work''', cc: '', from: '', replyTo: '', subject: 'Devops Pipeline', to: 'oumayma.bettaieb@esprit.tn'
            }
       }
      
         }
     }
     
     
