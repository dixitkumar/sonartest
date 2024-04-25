def splitModules(String moduleName) {
      String value = ''
      Map submodules = readYaml file: 'modules.yml'
      submodules.parcels."${moduleName}".each { module ->
        value = value + module + ','
    }
      return value.replaceAll(''',$''', '''''')
}

pipeline {
    agent any
    stages {
        stage('Stage 1') {
            steps {
                script {
                      Map submodules = readYaml file: 'modules.yml'
                      submodules.parcels.each { submodule ->
                      def moduleNames = splitModules(submodule.key)
                      stage(submodule.key){
                                      	bat "echo ${moduleNames}"
                      }
                }
                }
            }
        }
    }
}