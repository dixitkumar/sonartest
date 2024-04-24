def splitModules(String moduleName) {
      String value = ''
      Map submodules = readYaml file: 'modules.yml'
      println 'Loaded configuration values: \n\n' + JsonOutput.prettyPrint(JsonOutput.toJson(submodules))
      "submodules.parcels.${moduleName}.each" { module ->
      	echo 'Hello'
      	echo module
      	echo "${module}"
        value = value + module + ','
        echo 'Hello'
    }
    return value
     // return value.replaceAll(''',$''', '''''')
}

pipeline {
    agent any
    stages {
        stage('Stage 1') {
            steps {
                script {
                String accounting = splitModules('accounting')
                
               echo "${accounting}"
                }
            }
        }
    }
}