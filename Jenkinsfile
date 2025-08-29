pipeline {
    agent any

    post {
        always {
            emailext(
                to: 'joao.marcos@petzpartner.com.br',
                subject: 'Teste de envio',
                body: 'Este é um e-mail de teste enviado pelo Jenkins.',
                attachLog: true
            )
        }
    }
}