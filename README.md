# Atlantis

Plataforma web para organizar e acompanhar a preparação para concursos públicos — antes e depois da publicação do edital.

## Stack

- **Frontend:** Angular + TypeScript, Bootstrap
- **Backend:** Java 25 + Spring Boot
- **Banco de dados:** PostgreSQL 18, com migrações via Flyway
- **Ambiente local:** Docker Compose para o banco

## Estrutura

- `backend/`: API em Spring Boot
- `frontend/`: interface em Angular
- `docker-compose.yml`: serviços locais (PostgreSQL)

## Pré-requisitos

- Docker Desktop (com backend WSL2 no Windows)

## Subir o banco de dados

1. Copie o arquivo de exemplo e defina uma senha:

   ```powershell
   Copy-Item .env.example .env
   ```

   Edite o `.env` e troque o valor de `POSTGRES_PASSWORD`. O `.env` é local e não vai para o repositório.

2. Suba o contêiner em segundo plano:

   ```powershell
   docker compose up -d
   ```

3. Confira se o banco está saudável:

   ```powershell
   docker compose ps
   ```

   O status deve mostrar `healthy`.

## Comandos úteis

| Comando | O que faz |
|---|---|
| `docker compose up -d` | Sobe o banco em segundo plano |
| `docker compose ps` | Mostra o status dos serviços |
| `docker compose logs -f postgres` | Acompanha os logs do PostgreSQL |
| `docker compose stop` | Para o banco e mantém os dados |
| `docker compose down` | Remove os contêineres e mantém os dados |
| `docker compose down -v` | Remove contêineres **e apaga todos os dados** |

## Conexão

| Parâmetro | Valor |
|---|---|
| Host | `localhost` |
| Porta | `5432` (ou `POSTGRES_PORT`) |
| Banco | `atlantis` (ou `POSTGRES_DB`) |
| Usuário | `atlantis` (ou `POSTGRES_USER`) |
| Senha | valor de `POSTGRES_PASSWORD` no `.env` |

## Licença

Distribuído sob a licença MIT. Veja [`LICENSE`](LICENSE).

## Segurança

O projeto usa o [Gitleaks](https://github.com/gitleaks/gitleaks) (versão fixada em `v8.30.1`, executada pelo Docker) para bloquear commits com segredos. Depois de clonar, ative o hook uma vez:

```bash
git config core.hooksPath .githooks
```

Para verificar o histórico completo:

```bash
docker run --rm -v "$(pwd -W):/repo" ghcr.io/gitleaks/gitleaks:v8.30.1 git /repo --redact
```
