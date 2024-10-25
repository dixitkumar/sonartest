def splitModules(String moduleName) {
      String value = ''
      Map submodules = readYaml file: 'modules.yml'
      submodules.parcels."${moduleName}".each { module ->
        value = value + module + ','
    }
      return value.replaceAll(''',$''', '''''')
}
def generateReport(String reportName) {
  publishHTML target: [
  allowMissing: false,
  alwaysLinkToLastBuild: false,
  keepAll: true,
  reportDir: 'test',
  reportFiles: '**/*',
  reportName: " ${ reportName }"
  ]
    
}

pipeline {
    agent any
parameters {
        choice(name: 'autotest', choices: ['cede-autotest', 'fcr-autotest'], description: 'Pick something')
	choice(name: 'dbplatform', choices: ['mysql', 'postgresql', 'sqlserver', 'oracle'], description: 'Pick something')
	
    }
    stages {
	    stage("test"){
		    steps{
			    script{
				    echo "Hello"
				    def userex= "AT_UPR_SOURCE"
				    String userex1= userex.replace("SOURCE","TEST")
			    	    echo ${userex}
				    echo "bye"
			    }
		    
		    }
		    
	    }
        stage('Stage 1') {
            steps {
                script {
                      Map submodules = readYaml file: 'modules.yml'
                      submodules.parcels.each { submodule ->
                      def moduleNames = splitModules(submodule.key)
                      stage(submodule.key){
                                      	bat "echo ${moduleNames}"
                                                generateReport(submodule.key)
dir('test') {
		    			archiveArtifacts artifacts: "${submodule.key}", fingerprint: true   
		    		}
                          
                      }
                }
                }
            }
        }
    }
}
