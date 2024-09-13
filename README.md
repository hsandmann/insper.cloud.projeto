# insper.cloud.projeto

## CADASTRO
```mermaid
sequenceDiagram
    autonumber
    actor Alice
    Alice->>+App: registrar(email, senha, nome)
    App->>+Postgres: consulta email
    break se email encontrado
        Postgres-->>Alice: error 409
    end
    App->>Postgres: grava dados e hash da senha no bd
    App->>App: gera JWT Token
    App-->>-Alice: retorna JWT Token
````

## LOGIN
```mermaid
sequenceDiagram
    autonumber
    actor Alice
    Alice->>+App: login(email, senha)
    App->>+Postgres: consulta email e hash no db
    break se email não encontrado
        Postgres-->>Alice: error 401
    end
    break se email e senha não confere
        Postgres-->>Alice: error 401
    end
    App->>App: gera JWT Token
    App-->>-Alice: retorna JWT Token

```

## DADOS
```mermaid
sequenceDiagram
    autonumber
    actor Alice
    Alice->>+App: solicita base (com JWT)
    App-->>App: verifica permissão do JWT
    break se JWT ausente ou corrompido
        App-->>Alice: error 403
    end
    App-->>App: 3th party (web scraping)<br>solicita dados de uma base ou página
    Note right of App: Adquire dados da internet, <br>fazendo scraping de quaisquer<br> dados interessantes para o aluno.<br>O conteúdo deve ter atualização frequente.
    App->>Kafka: envia mensagem de registro de acesso
    par
        Kafka--XAppLogger: registra acesso ao sistema
        AppLogger->>MongoDB: grava na base
    end
    App-->>-Alice: retorna dados
```

## Docker Compose
```mermaid
flowchart LR
  subgraph docker compose
    direction TB
    App
    AppLogger
    Kafka
    Postgres
    MongoDB
  end
```