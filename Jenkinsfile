pipeline {
    agent any

    parameters {
        string(defaultValue: 'https://raw.githubusercontent.com/elastic/examples/master/Common%20Data%20Formats/apache_logs/apache_logs', description: 'URL del archivo de log', name: 'logURL')
    }

    stages {
        stage('Descargar archivo de log') {
            steps {
                script {
                    def file = downloadLogFile(params.logURL)
                    if (file) {
                        echo "Archivo de log descargado exitosamente."
                    } else {
                        error "No se pudo descargar el archivo de log."
                    }
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

def downloadLogFile(logURL) {
    def response = httpRequest(url: logURL)
    if (response.status == 200) {
        writeFile file: 'apache_logs.txt', text: response.content
        return true
    } else {
        return false
    }
}

