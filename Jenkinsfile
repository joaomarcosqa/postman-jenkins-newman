pipeline {
    agent any

    tools {
        nodejs 'NodeJS_LTS'
    }

    environment {
        COLLECTION = 'tests/collection.postman_collection.json'
        REPORT_DIR = 'results'
        REPORT_FILE = 'results/report.xml'
    }

    stages {
        stage('Instalar Newman') {
            steps {
                sh 'npm install -g newman'
            }
        }

        stage('Executar Collection sem Variáveis') {
            steps {
                sh '''
                    mkdir -p ${REPORT_DIR}
                    newman run ${COLLECTION} \
                        --reporters cli,junit \
                        --reporter-junit-export=${REPORT_FILE}
                '''
            }
        }
    }

}