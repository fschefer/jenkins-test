pipeline {
    agent any

    stages {
        stage('Instalar Newman') {
            steps {
                bat 'npm install -g newman'
            }
        }

        stage('Executar testes com Newman') {
            steps {
                bat 'newman run "jsonplaceholder-api-tests.json"'
            }
        }
    }
}