pipeline {
    agent any

    stages {
        stage('Instalar Dependências') {
            steps {
                bat 'npm install'
            }
        }

        stage('Iniciar API Local') {
            steps {
                bat 'start "API Local" cmd /c "npx json-server --watch db.json"'
                bat 'timeout /t 5'
            }
        }

        stage('Executar Testes com Newman') {
            steps {
                bat 'npx newman run "JSONPlaceholder API Tests.postman_collection.json" --environment="local.postman_environment.json"'
            }
        }
    }
    post {
        always {
            echo 'Tentando parar a API local...'
            bat 'taskkill /IM node.exe /F || echo "Processo node não encontrado para parar."'
        }
    }
}