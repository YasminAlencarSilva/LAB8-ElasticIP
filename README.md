# LAB8 – Elastic IP e API em Docker

## Objetivo

Este laboratorio demonstra a conteinerizacao de uma API Python com FastAPI e sua preparacao para implantacao em uma instancia EC2 com Elastic IP.

## Tecnologias

- Python 3.11
- FastAPI e Uvicorn
- Docker
- Docker Hub
- GitHub Actions
- AWS EC2 e Elastic IP

## Estrutura

```text
LAB8-ElasticIP/
├── .github/
│   └── workflows/
│       ├── docker-hub.yml
│       └── python-app.yml
├── app/
│   └── main.py
├── tests/
│   └── test_main.py
├── .dockerignore
├── Dockerfile
└── requirements.txt
```

## Executar localmente

Instale as dependencias:

```bash
python -m pip install -r requirements.txt
python -m pip install pytest httpx
```

Inicie a API:

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8080
```

Acesse `http://localhost:8080` e a documentacao interativa em `http://localhost:8080/docs`. O endpoint `/health` retorna o estado de saude da API.

## Executar testes

```bash
PYTHONPATH=. pytest tests/ -v
```

## Construir e executar com Docker

```bash
docker build -t lab8-api:1.0 .
docker run -d --name lab8-api -p 8080:8080 lab8-api:1.0
```

## GitHub Actions

O workflow `python-app.yml` executa os testes automatizados e valida a construcao da imagem Docker nos pushes para `main` e `develop`.

O workflow `docker-hub.yml` publica a imagem `yasminalencar/lab8-api:1.0` no Docker Hub quando ha push na branch `main`. Configure os secrets `DOCKERHUB_USERNAME` e `DOCKERHUB_TOKEN` nas configuracoes do repositorio.

A publicacao no Docker Hub e mantida em um unico workflow para evitar builds e pushes duplicados.

## AWS EC2 e Elastic IP

Apos publicar a imagem, ela pode ser executada na instancia EC2. Garanta que a instancia permita o trafego TCP na porta 8080 e que o Elastic IP esteja associado a instancia correta.

Exemplo de execucao na EC2:

```bash
docker pull yasminalencar/lab8-api:1.0
docker run -d --name lab8-api --restart unless-stopped -p 8080:8080 yasminalencar/lab8-api:1.0
```

## Repositorio

https://github.com/YasminAlencarSilva/LAB8-ElasticIP
