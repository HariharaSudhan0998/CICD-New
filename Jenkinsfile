pipeline {
   agent any

   stages {
    stage('Compile') {
     steps {
        sh(script: 'mvn compile')
        echo 'Compile...'
     }
   }
    stage('Unit Test') {
     steps {
        sh(script: 'mvn test')
	sh(script: 'mvn package')
	 junit 'target/surefire-reports/*.xml'


//junit 'more-test-results.xml'
        echo 'Unit Test...'
     }
   }
    stage('Code Quality') {
     steps {	    	    
           withSonarQubeEnv('sonarqube') {
		     sh """ 
		         mvn clean install
                        mvn sonar:sonar \
                          -Dsonar.projectKey=sonarqube1 \
                          -Dsonar.host.url=http://65.2.108.33:9000 \
                          -Dsonar.login=eddc17c6929a3401c0f774a0d24563c7419106b7
                       """ 
		        } 
        
        echo 'Code Quality...'
	}
   }
    stage('Artifact Push') {
     steps {	          
	   //  sh(script: 'mvn  -version')
             //sh(script: 'mvn   deploy')
	     
        echo 'Artifact Push...'
     }
   }
    stage('Deploy') {
	      steps{
		    script {
               sshagent (['22a85fad-8bf3-478b-8daf-468fbf902abe']) {
		    sh """                   
                     wget http://65.1.231.149:8081/repository/spring-boot1/org/springframework/gs-spring-boot/1.0.1/gs-spring-boot-1.0.1.jar
		     
		    nohup java -jar gs-spring-boot-1.0.1.jar  --server.port=8083
		     
		      """
		   }                 
	      } 
        }
   }
    stage('Smoke Test') {
     steps {       			         
			//  sh ( 'curl:http://65.2.108.33:8080'  )	 
	     // curl -u admin:devops123 -d "script=println InetAddress.localHost.hostAddress" http://65.2.108.33:8080
	     //      sh 'curl http://65.2.108.33:8080'
		     
        echo 'Smoke Test...'
		     }
   }
    stage('Functional Test') {
     steps {	     
				/*      checkout scm
				
				script{
				      sh(/mvn clean  test /)
				   } */
				
				      // step([$class : 'Publisher', reportFilenamePattern : '**/testng-results.xml'])  
	           
			
        echo 'Functional Test...'
     }
   }
   stage('Email Notification') {
     steps {
	    // mail bcc: '', body: '''Hi all,
              //The pipeline run successfully.''', cc: '', from: '', replyTo: '', subject: 'Jenkins pipeline', to: 'hariharasudhan9894@gmail.com'
        echo 'Email Notification...'
     }
   }
  }
}
