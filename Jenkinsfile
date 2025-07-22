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
				  def username = 'Jenkins_SOURCE'
				    def test = "${username}".replace("SOURCE","TEST")

echo "I said, Hello Mr. ${test}"
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
	    post { 
        always { 
            echo 'I will always say Hello again!'
            	 
                        	def props = new Properties()
							def file = new File('./build.properties')
							file.withInputStream { stream ->
							    props.load(stream)
							}
							sicsBuildNo = props.getProperty('build')
							println "SicsBuildNo: $sicsBuildNo"
                  
        }
    }
}
