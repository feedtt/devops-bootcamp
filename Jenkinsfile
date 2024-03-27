pipeline {
    agent any
    
    environment {
        DEPARTMENT = 'tecnologia' // Departamento por defecto
    }
    
    parameters {
        string(name: 'LOGIN', defaultValue: '', description: 'Ingrese el login del usuario')
        string(name: 'NAME', defaultValue: '', description: 'Ingrese el nombre del usuario')
        string(name: 'DEPARTMENT', defaultValue: '', description: 'Ingrese el departamento del usuario: contabilidad, finanzas o tecnologia')
    }
    
    stages {
        stage('Crear Usuario') {
            steps {
                script {
                    def password = sh(script: "openssl rand -base64 12", returnStdout: true).trim() // Genera una contraseña temporal
                    sh "sudo useradd -m -s /bin/bash -c '${params.NAME}' ${params.LOGIN}" // Crea el usuario
                    sh "echo '${params.LOGIN}:${password}' | sudo chpasswd" // Asigna la contraseña al usuario
                }
            }
        }
        
        stage('Enviar Contraseña por Email') {
            when {
                expression { params.LOGIN != '' && params.NAME != '' && params.DEPARTMENT != '' }
            }
            steps {
                echo "Contraseña temporal para ${params.LOGIN}: ${password}" // Muestra la contraseña temporal
                // Aquí añadirías la lógica para enviar la contraseña por correo electrónico
            }
        }
    }
}


