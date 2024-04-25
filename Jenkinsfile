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
                def accounting = splitModules('accounting')
                echo "${accounting}"
                sh 'echo '''${accounting}''''
                }
            }
        }
    }
}