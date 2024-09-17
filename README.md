# Insper > Cloud >> Projeto

O projeto é dividido em 2 partes:

1. **Aplication Backend**: API RESTful em Node.js com Express e Postgres.
2. **Frontend**: Aplicação em React.js.

``` bash
source ./venv/bin/activate
```

## Aplicativo

### Instalação
```bash
{
    "nome": "Disciplina Cloud",
    "email": "cloud@insper.edu.br",
    "senha": "cloud0"
}
```

### CADASTRO
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
```

### LOGIN
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
    App-->>App: web scraping<br>solicita dados de uma base ou página<br>de um 3th party
    Note right of App: Adquire dados da internet, <br>fazendo scraping de quaisquer<br> dados interessantes para o aluno.<br>O conteúdo deve ter atualização frequente.
    App-->>-Alice: retorna dados
```

## Docker Compose
```mermaid
flowchart LR
  subgraph docker compose
    direction TB
    App --> Postgres
    Postgres --> App
  end
```