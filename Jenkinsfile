pipeline {
    agent any

    stages {
        stage('Instalar Newman') {
            steps {
                sh 'npm install -g newman'
            }
        }

        stage('Executar Collection sem Variáveis') {
            steps {
                sh '''
                    mkdir -p results
                    newman run tests/collection.postman_collection.json \
                        --reporters cli,junit \
                        --reporter-junit-export=results/report.xml
                '''
            }
        }
    }

    post {
        always {
            junit 'results/report.xml'
        }
    }
}
