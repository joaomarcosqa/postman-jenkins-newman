pipeline {
  agent any
  tools { nodejs 'NodeJS_LTS' }

  options {
    timestamps()
    // ansiColor('xterm') <-- REMOVIDO
  }

  environment {
    COLLECTION  = 'tests/collection.postman_collection.json'
    REPORT_DIR  = 'results'
    REPORT_XML  = 'results/report.xml'
    REPORT_HTML = 'results/report.html'
  }

  stages {
    stage('Instalar Newman + htmlextra') {
      steps {
        sh '''
          npm --version
          node --version
          npm install -g newman newman-reporter-htmlextra
          newman -v
        '''
      }
    }

    stage('Executar Collection (sem ambientes)') {
      steps {
        sh '''
          test -f "${COLLECTION}" || { echo "Collection não encontrada: ${COLLECTION}"; exit 2; }

          mkdir -p "${REPORT_DIR}"
          newman run "${COLLECTION}" \
            --reporters cli,junit,htmlextra \
            --reporter-junit-export="${REPORT_XML}" \
            --reporter-htmlextra-export="${REPORT_HTML}"
        '''
      }
    }
  }

  post {
    always {
      junit "${REPORT_XML}"
      archiveArtifacts artifacts: "results/*", onlyIfSuccessful: false
    }
  }
}
