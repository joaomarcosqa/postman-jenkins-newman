pipeline {
    agent any

    tools {
        nodejs 'NodeJS_LTS' // Nome definido na configuração de Tools no Jenkins
    }

    environment {
        COLLECTION = 'tests/collection.postman_collection.json'
        REPORT_DIR = 'results'
        REPORT_FILE = "${REPORT_DIR}/report.xml"
    }

    stages {
        stage('Executar Collection') {
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

    post {
        always {
            junit "${REPORT_FILE}"
        }
    }
}