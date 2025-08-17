# chatollama

<img src="https://github.com/ollama/ollama/blob/main/docs/logo.svg" alt="Ollama" width="100" />

Projeto para experimentos com DSA (Data Science / APIs) composto por dois serviços:

- `dsa_api/` — API Python (FastAPI/Flask, conforme implementado no código) para endpoints de processamento.
- `dsa_streamlit_app/` — Aplicação Streamlit para interface web interativa.

Este README descreve como configurar, executar e desenvolver o projeto localmente e com Docker.

## Sumário

- [Visão geral](#vis%C3%A3o-geral)
- [Estrutura do repositório](#estrutura-do-reposit%C3%B3rio)
- [Pré-requisitos](#pr%C3%A9-requisitos)
- [Execução rápida (Docker Compose)](#execu%C3%A7%C3%A3o-r%C3%A1pida-docker-compose)
- [Execução individual dos serviços](#execu%C3%A7%C3%A3o-individual-dos-servi%C3%A7os)
- [Desenvolvimento local](#desenvolvimento-local)
- [Variáveis de ambiente](#vari%C3%A1veis-de-ambiente)
- [Como contribuir](#como-contribuir)
- [Licença e contato](#licen%C3%A7a-e-contato)

## Visão geral

`chatollama` é um repositório para rápido desenvolvimento e deploy de uma API de processamento (em `dsa_api`) e uma interface Streamlit (em `dsa_streamlit_app`). O objetivo é permitir iteração rápida localmente usando o Python e deployment simples com Docker Compose.

## Estrutura do repositório

Raiz:

- `docker-compose.yml` — composição dos serviços (API + Streamlit) para desenvolvimento e/ou produção.
- `dsa_api/` — código-fonte da API (ex.: `app.py`, `requirements.txt`, `Dockerfile`).
- `dsa_streamlit_app/` — app Streamlit (ex.: `app.py`, `requirements.txt`, `Dockerfile`).
- `.gitignore` — regras para ignorar arquivos não versionados.

Observe os diretórios `dsa_api` e `dsa_streamlit_app` para detalhes de implementação.

## Pré-requisitos

- Docker e Docker Compose instalados (versão compatível com o `docker-compose.yml`).
- Python 3.8+ para execução local sem Docker (se for utilizado).
- Recomenda-se criar um ambiente virtual para desenvolvimento local.

## Execução rápida (Docker Compose)

A forma mais simples de executar o projeto em desenvolvimento ou teste é usar o `docker-compose` na raiz do projeto:

```bash
# subir todos os serviços em foreground
docker compose up --build

# ou rodar em background (detached)
docker compose up -d --build

# parar e remover containers
docker compose down
```

Os serviços e portas expostas são definidas em `docker-compose.yml`. Após subir, acesse a UI Streamlit e a API pelos endereços/portas configurados.

## Execução individual dos serviços

### dsa_api (local)

1. Acesse o diretório:

```bash
cd dsa_api
```

2. Instale dependências (recomenda-se virtualenv):

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

3. Execute a API (exemplo):

```bash
# Exemplo genérico caso o app seja FastAPI
uvicorn app:app --reload --host 0.0.0.0 --port 8000

# ou, se for Flask
# FLASK_APP=app.py flask run --host=0.0.0.0 --port=8000
```

### dsa_streamlit_app (local)

1. Acesse o diretório:

```bash
cd dsa_streamlit_app
```

2. Instale dependências:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

3. Execute o Streamlit:

```bash
streamlit run app.py --server.port 8501
```

## Variáveis de ambiente

Coloque configurações sensíveis e endpoints em arquivos `.env` (não commitados). Exemplos típicos:

- `API_HOST` / `API_PORT`
- `STREAMLIT_HOST` / `STREAMLIT_PORT`
- chaves de serviços externos (ex.: `OPENAI_API_KEY`, `AWS_ACCESS_KEY_ID`)

Garanta que `.gitignore` inclui `*.env` (já presente no repositório) para evitar vazamento de segredos.

## Desenvolvimento e dicas

- Para iterar rapidamente, use `docker compose up --build` com `--watch`/`--reload` habilitado nos containers (ex.: `uvicorn --reload`).
- Faça pequenos commits com mensagens descritivas.
- Teste endpoints manualmente com `curl` ou ferramentas como Postman/HTTPie.
- Coloque scripts de inicialização no `docker-compose.yml` para padronizar comportamento.

## Como contribuir

1. Fork o projeto.
2. Crie uma branch de feature: `git checkout -b feat/minha-feature`.
3. Faça commits atomizados e com mensagens claras.
4. Abra pull request descrevendo a motivação e o que foi implementado.

## Licença e contato

Adicione aqui a licença do projeto (ex.: MIT) se desejar. Para perguntas ou suporte, abra uma issue neste repositório ou contate o mantenedor.

---

Se quiser, eu posso:

- adaptar o README com detalhes específicos extraídos de `LEIAME.txt` ou dos `app.py` dentro dos subdiretórios (rotas, portas reais, requisitos específicos);
- adicionar um `Makefile` ou `tasks.json` para comandos comuns;
- criar o commit inicial com este README e o `.gitignore` e dar push para o remoto configurado.

Diga qual das opções prefere que eu execute em seguida.
