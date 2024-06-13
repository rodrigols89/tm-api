 - Notes on what I learned in course [FastAPI do ZERO (PT-BR)](https://fastapidozero.dunossauro.com/).
 - All notes here will be in Portuguese (Brazil).

# FastAPI do ZERO (PT-BR)

## Conteúdo


 - **FastAPI Settings & Management:**
   - Como iniciar o servidor a partir do FastAPI `(fastapi dev app.py)`
   - [Entendendo o "Uvicorn"](#intro-to-uvicorn)
   - [](#)
   - [](#)
 - **Project Settings:**
   - [Como abrir um script no modo Interativo](#py-interactive-mode)
   - [Como criar grupos na instalação do Poetry (---group)](#poetry-group)
   - [Como configurar o "Ruff" para analisar o seu código](#ruff-settings)
   - [Entendendo os comandos "Ruff"](#ruff-commands)
   - [](#)
   - [](#)















<!--- ( FastAPI Settings & Management ) --->

---

<div id="intro-to-uvicorn"></div>

## Entendendo o "Uvicorn"

> Embora o FastAPI tenha uma aplicação de terminal que facilita a execução. Para podermos acessar essas APIs por um navegador ou de outras aplicações clientes, é necessário um servidor.

 - É aí que o *"Uvicorn"* entra em cena. *Ele atua como esse servidor*, disponibilizando a API do FastAPI em rede. Isso permite que a API seja acessada de outros dispositivos ou programas.
 - Sempre que usarmos o fastapi para inicializar a aplicação no shell, ele faz uma chamada interna para inicializar o uvicorn. Por esse motivo ele aparece nas respostas HTTP e também na execução do comando.

---









































<!--- ( Project Settings ) --->

---

<div id="py-interactive-mode"></div>

## Como abrir um script no modo Interativo

Para abrir o terminal interativo com o seu código carregado, você deve chamar o Python no terminal usando `-i`:

```bash
python -i <seu_arquivo.py>
```

**NOTE:**  
O interpretador do Python executa o código do arquivo e retorna o shell após executar tudo que está escrito no arquivo.

---

<div id="poetry-group"></div>

## Como criar grupos na instalação do Poetry

Ao instalar novas bibliotecas no nosso projeto, podemos especificar a qual grupo essas bibliotecas pertence. Para isso, basta adicionar a flag `--group` na hora da instalação:

```bash
poetry add --group dev pytest@latest pytest-cov@latest taskipy@latest ruff@latest httpx@latest
```

---

<div id="ruff-settings"></div>

## Como configurar o "Ruff" para analisar o seu código

```toml
[tool.ruff]
line-length = 79

[tool.ruff.lint]
preview = true
select = ['I', 'F', 'E', 'W', 'PL', 'PT']
ignore = ['E402', 'F811']

[tool.ruff.format]
preview = true
quote-style = 'single'
```

 - `[tool.ruff]: Configurações Globais do Ruff.`
   - `extend-exclude = ['migrations']  # Exclude migrations folder from linting.`
 - `[tool.ruff.lint]: Análise de Linter.`
   - **select:**
     - `I` ([Isort](https://pycqa.github.io/isort/){:target="_blank"}): Checagem de ordenação de imports em ordem alfabética
     - `F` ([Pyflakes](https://github.com/PyCQA/pyflakes){:target="_blank"}): Procura por alguns erros em relação a boas práticas de código
     - `E` (Erros [pycodestyle](https://pycodestyle.pycqa.org/en/latest/){:target="_blank"}): Erros de estilo de código
     - `W` (Avisos [pycodestyle](https://pycodestyle.pycqa.org/en/latest/){:target="_blank"}): Avisos de coisas não recomendadas no estilo de código
     - `PL` ([Pylint](https://pylint.pycqa.org/en/latest/index.html){:target="_blank"}): Como o `F`, também procura por erros em relação a boas práticas de código
     - `PT` ([flake8-pytest](https://pypi.org/project/flake8-pytest-style/){:target="_blank"}): Checagem de boas práticas do Pytest
 - `[tool.ruff.format]: Formatação (Formatter) do Ruff.`
   - **NOTE:** Lembrando que a opção de usar aspas simples é totalmente pessoal, você pode usar aspas duplas se quiser.

---

<div id="ruff-commands"></div>

## Entendendo os comandos "Ruff"

Nós criamos vários comandos Ruff com o Taskipy. Agora vamos ver e entender eles:

```toml
lint = 'ruff check . && ruff check . --diff'
format = 'ruff check . --fix && ruff format .'
pre_test = 'task lint'
```

Os comandos definidos fazem o seguinte:

 - **lint: Executa duas variações da checagem**
   - `ruff check`: Mostra os códigos de infrações de boas práticas.
   - `ruff check --diff`: Mostra o que precisa ser alterado no código para que as boas práticas sejam seguidas.
   - `&&`: O duplo `&` faz com que a segunda parte do comando só seja executada se a primeira não der erro. Sendo assim, enquanto o `--diff` apresentar erros, ele não executará o `check`
 - **format: Executa duas variações da formatação**
   - `ruff check . --fix`: Faz algumas correções de boas práticas automaticamente.
   - `ruff format`: Executa a formatação do código em relação as convenções de estilo de código

---
















































---

Ro**drigo** **L**eite da **S**ilva - **drigols**
