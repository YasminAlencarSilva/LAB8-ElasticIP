# LAB9 – Pipeline CI/CD

## Sobre o projeto

Este projeto apresenta a evolução de um pipeline de Integração Contínua e Entrega Contínua (CI/CD), utilizando GitHub Actions, Python, Docker e Docker Hub.

O objetivo é automatizar os testes da aplicação, construir e publicar imagens Docker e separar os processos de homologação e produção.

## Tecnologias utilizadas

- Python 3.11
- FastAPI
- Docker
- Docker Hub
- GitHub Actions
- Git e GitHub

## Fluxo do pipeline

### Branch develop – Homologação

1. O desenvolvedor realiza um push na branch `develop`.
2. O GitHub Actions executa o build e os testes.
3. A imagem Docker é construída e publicada no Docker Hub.
4. O pipeline verifica se a imagem foi publicada corretamente.
5. A validação de homologação é executada automaticamente.

### Branch main – Produção

1. O desenvolvedor realiza um push na branch `main`.
2. O GitHub Actions executa o build e os testes.
3. A imagem Docker é construída e publicada no Docker Hub.
4. O ambiente de produção exige aprovação manual.
5. Após a aprovação, o pipeline verifica a imagem publicada.

## Ambientes configurados

- `Homologacao`: ambiente destinado à validação automática.
- `Producao`: ambiente protegido por aprovação manual.

## Estrutura do projeto

```text
LAB8-ElasticIP/
├── .github/
│   └── workflows/
│       ├── docker-hub.yml
│       └── python-app.yml
├── app/
├── tests/
├── .dockerignore
├── .gitignore
├── Dockerfile
└── requirements.txt
```

## Resultados dos testes

- Build e testes automatizados executados com sucesso.
- Imagem Docker publicada no Docker Hub.
- Validação de homologação executada na branch `develop`.
- Aprovação e validação de produção executadas na branch `main`.

## Situação da infraestrutura

O pipeline de build, publicação e validação das imagens foi testado no GitHub Actions.

A implantação real nas instâncias EC2 permanece pendente de configuração e acesso à infraestrutura AWS.

## Repositório

GitHub: https://github.com/YasminAlencarSilva/LAB8-ElasticIP
