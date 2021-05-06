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
	      sh(script: 'mvn  -version')
              sh(script: 'mvn   deploy')
	     
        echo 'Artifact Push...'
     }
   }
    stage('Deploy') {
     steps {	                         
	     
	    // sh(deploy contextPath: 'http://65.1.231.149:8081/repository/spring-boot1/org/springframework/gs-spring-boot/1.0.1/gs-spring-boot-1.0.1.jar', 
	      //    war: 'gs-spring-boot-1.0.1.jar')	   
        echo 'Deploy...'
     }
   }
    stage('Smoke Test') {
     steps {       			         
			   //  sh "./smoke_test.sh"   
		     
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
