pipeline {
    agent any

    stages {
        stage('Instalar Dependências') {
            steps {
                bat 'npm install'
            }
        }

        stage('Executar Testes com API Local') {
            steps {
                script {
                    try {
                        // Inicia o servidor em segundo plano
                        bat 'start "API Local" cmd /c "npx json-server --watch db.json --host 127.0.0.1"'
                        
                        // Espera o servidor iniciar
                        bat 'ping -n 21 127.0.0.1 > nul'

                        // Roda os testes
                        bat 'npx newman run "jsonplaceholder-api-tests.json" --environment="local.postman_environment.json"'
                    }
                    finally {
                        // Este bloco SEMPRE será executado após o 'try',
                        // garantindo a finalização do servidor.
                        echo 'Finalizando o processo do servidor local...'
                        bat 'taskkill /IM node.exe /F /FI "WINDOWTITLE eq API Local"'
                    }
                }
            }
        }
    }
}