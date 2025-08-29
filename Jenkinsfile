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
            junit "${REPORT_FILE}"

            script {
                emailext(
                    subject: "[${currentBuild.currentResult}] ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                    body: """<p>Pipeline finalizada com status: <strong>${currentBuild.currentResult}</strong></p>
                             <p><b>Job:</b> ${env.JOB_NAME}</p>
                             <p><b>Build:</b> #${env.BUILD_NUMBER}</p>
                             <p><b>Link:</b> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>""",
                    to: 'yjoaomarcosadm@outlook.com',
                    attachLog: true
                )
            }
        }
    }
}