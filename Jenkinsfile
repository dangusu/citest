//CODE_CHANGES = getGitChanges() // a groovy sscript that checks if are changes and return boolean


pipeline {

  agent any

  environment{  //definim env variables aici
        NEW_VERSION = '1.3.0' //se poate calcula, extrasa din cod, am scris direct
        SERVER_CREDENTIALS = credentials('app-pipeline') //plugin de binding de crdentials
  }
  
  stages {
  
      stage("build") {
          when { // executa stageul asta doar WHEN EXPRESSION e true, daca nu, skip
                      expression {
                          env.BRANCH_NAME=='dev' //&& CODE_CHANGES == true //code_changes se defineste outside pipeline
                          }
                    }
          steps {
            echo 'building the app'    
          }
	}
          
       stage("test") {
          when { // executa stageul asta doar WHEN EXPRESSION e true, daca nu, skip
            expression {
                env.BRANCH_NAME=='main' || BRANCH_NAME=='master'
                }
          }
          steps {
            echo 'testing the app'
            echo "testing version ${NEW_VERSION}" //variabilele se scriu in double quotes, var delcar in environment
            echo "testing with ${SERVER_CREDENTIALS}"
            pwsh "{SERVER_CREDENTIALS}"

            withCredentials([

                usernamePassword(credentials: 'app-pipeline', usernameVariable: USER, passwordVariable:PWD)
                // takes the crdentials from app-pipelaine si le salveaza in variabila USER si PWD
            ]){
                pwsh "some script ${USER}"
            }

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
                echo 'post de always'
            }
            success { echo 'a ajuns la success'}
            failure { echo 'a ajuns la failure'}
        }
	

  }
