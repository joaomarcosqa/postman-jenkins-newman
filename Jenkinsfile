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

    post {
        always {
            // Publicar relatório JUnit
            junit "${REPORT_FILE}"

            // Enviar e-mail
            emailext(
                subject: "[${BUILD_STATUS}] ${JOB_NAME} - Build #${BUILD_NUMBER}",
                body: """<p>Pipeline finalizada com status: <strong>${BUILD_STATUS}</strong></p>
                        <p><b>Job:</b> ${JOB_NAME}</p>
                        <p><b>Build:</b> #${BUILD_NUMBER}</p>
                        <p><b>Link:</b> <a href="${BUILD_URL}">${BUILD_URL}</a></p>""",
                to: 'yjoaomarcosadm@outlook.com,testechpaterqa@gmail.com',
                attachLog: true
            )
        }
    }
}