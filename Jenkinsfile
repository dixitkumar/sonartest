def splitModules(String moduleName) {
      String value = ''
      Map submodules = readYaml file: 'modules.yml'
      submodules.parcels."${moduleName}".each { module ->
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