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
	choice(name: 'dbPlatform', choices: ['mysql', 'sqlserver, 'postgresql', 'oracle'], description: 'Pick something')
        booleanParam(name: 'do_import_databases', defaultValue: false, description: 'Import Databases')
    }
    stages {
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
