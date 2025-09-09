# Testes Postman no Jenkins (SEM ambientes)

## 📌 Objetivo
Este projeto demonstra como executar uma collection do Postman dentro de um pipeline do Jenkins utilizando o **Newman**.  
A ideia é rodar todos os testes da collection em um único ambiente padrão, sem alternar variáveis externas.

## 📂 Estrutura do projeto
```bash
├─ Jenkinsfile
└─ tests/
   └─ collection.postman_collection.json
Jenkinsfile: define o pipeline no Jenkins para rodar a collection.

tests/collection.postman_collection.json: collection exportada do Postman contendo os requests e testes.

⚙️ Funcionamento
O Jenkins instala o Newman e o reporter htmlextra.

A collection é executada integralmente em um único ambiente fixo.

São gerados relatórios em:

JUnit XML → para integração com o Jenkins (resultados de testes).

HTML → relatório detalhado para análise manual.

O Jenkins publica os relatórios como artefatos, permitindo o download e visualização no console do job.

▶️ Benefícios
Automação simples e rápida para collections do Postman.

Integração direta com a aba de testes do Jenkins.

Relatório visual em HTML para fácil inspeção de falhas.