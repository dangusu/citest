pipeline {

  agent any
  
  stages {
  
      stage("build") {
          
          steps {
            echo 'building the app'    
          }
	}
          
       stage("test") {
          
          steps {
            echo 'testing the app' 
          }
	}
       
        stage("deploy") {
          
          steps {
            echo 'deploying the app' 
          }
	}
      }
	
	post { // BUILD STATUS or BUILD STATUS CHANGE
		always {
			//dupa STAGES face ALWAYS something
		}
		success {}
		failure {}
	}	
	

  }
