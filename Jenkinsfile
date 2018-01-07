pipeline {
	agent any
	tools {
		maven 'M3' 
		jdk 'jdk8u125'
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
			checkout scm
		  }
		}

			stage('generate-resources'){
				steps{
			sh "mvn generate-resources"
		  }
			}

		stage('Deploy asciidoc'){
			steps{
				sh "cp -R target/generated-docs/* ${env.publicApacheRoot}"
			}
		}            
	}
	
	post{
        always{
             cleanWs()
        }
    }

}