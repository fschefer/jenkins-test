pipeline {
    agent any

    stages {
        stage('Instalar Dependências') {
            steps {
                bat 'npm install'
            }
        }

        stage('Executar Testes e API Local em Paralelo') {
            parallel {
                stage('Iniciar API Local') {
                    steps {
                        bat 'npx json-server --watch db.json --host 127.0.0.1'
                    }
                }
                stage('Executar Testes com Newman') {
                    steps {
                        bat 'ping -n 20 127.0.0.1 > nul'
                        bat 'npx newman run "jsonplaceholder-api-tests.json" --environment="local.postman_environment.json"'
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Finalizando todos os processos node.exe para limpeza...'
            bat 'taskkill /IM node.exe /F || echo "Nenhum processo node.exe encontrado para finalizar."'
        }
    }
}