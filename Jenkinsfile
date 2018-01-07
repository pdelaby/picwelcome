pipeline {
    agent any
    tools {
        maven 'M3' 
        jdk 'jdk8u125'
		npm 'nodeJs'
    }
	
    stages { 
             
		stage('Env') {
			steps{
				configFileProvider([configFile(fileId:'apache-conf', variable: 'apacheConfFile')]) {
					script{
						def apacheConf = readJSON(text: readFile(file: apacheConfFile))
						env.publicApacheRoot = "$apacheConf.publichtml.root"
					}
				}
			}
		}
		
		stage('Checkout'){
			steps{
				git "https://github.com/pdelaby/demo-rest-front.git"
			}
		}
  
        stage('Npm'){
            steps{
				sh "npm -v"
			}
        }

    }
	
	post{
        always{
             cleanWs()
        }
    }
   
}