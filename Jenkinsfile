pipeline {
    agent any

    parameters {
        string(defaultValue: 'https://raw.githubusercontent.com/elastic/examples/master/Common%Data%20Formats/apache_logs/apache_logs', description: 'URL del archivo de log', name: 'logURL')
    }

    stages {
        stage('Descargar archivo de log') {
            steps {
                script {
                    sh "curl -o apache_logs.txt ${params.logURL}"
                }
            }
        }

        stage('Contar solicitudes') {
            steps {
                script {
                    def logLines = readFile('apache_logs.txt').split('\n')
                    def count = logLines.findAll { line ->
                        line.contains('logstash') && line.contains('200')
                    }.size()
                    echo "El número de solicitudes con el nombre logstash y código de respuesta 200 es: ${count}"
                }
            }
        }
    }
}


