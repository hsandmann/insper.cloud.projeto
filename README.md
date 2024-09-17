# Insper > Cloud >> Projeto

A documentação desse site está disponível em [https://hsandmann.github.io/insper.cloud.projeto/](https://hsandmann.github.io/insper.cloud.projeto/).

## Setup

Para utilizar o código deste repositório, siga as instruções a seguir:

Crie um ambiente virtual do Python:

``` shell
python3 -m venv env
```

Ative o ambiente virtual (**você deve fazer isso sempre que for executar algum script deste repositório**):

``` bash
source ./env/bin/activate
```

Instale as dependências com:

``` shell
pip3 install -r requirements.txt
```

## Deployment

O material utiliza o mkdocs para gerar a documentação. Para visualizar a documentação, execute o comando:

``` bash
mkdocs serve
```

Para subir ao GitHub Pages, execute o comando:

``` bash
mkdocs gh-deploy
```
