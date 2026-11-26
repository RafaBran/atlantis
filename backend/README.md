# Backend

API em Spring Boot 4.1 com Java 25, Maven, Flyway e PostgreSQL.

## Pré-requisitos

- Banco no ar: na raiz do projeto, `docker compose up -d`.
- JDK 25 do projeto em `../.tools/jdk-25.0.5.1+2` (não vai para o repositório).

## Compilar

Este projeto usa um settings do Maven próprio (`.mvn/settings.xml`) e um cache próprio (`.mvn/repository`), sem alterar `~/.m2`. Rode na pasta `backend`:

```powershell
$env:JAVA_HOME = (Resolve-Path ..\.tools\jdk-25.0.5.1+2).Path
.\mvnw.cmd -s .mvn\settings.xml "-Dmaven.repo.local=.mvn\repository" -DskipTests package
```

No IntelliJ, em **Settings → Build, Execution, Deployment → Build Tools → Maven**, configure o **User settings file** como `backend\.mvn\settings.xml` apenas para este projeto.
