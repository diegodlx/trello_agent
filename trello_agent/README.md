# Trello Task Manager Agent

Agente de organizacao de tarefas integrado ao Trello, desenvolvido em Python com Google ADK. O projeto permite criar cards, listar tarefas e atualizar o status de atividades em um board do Trello por meio de um agente conversacional.

## Visao geral

Este projeto foi criado para automatizar a organizacao de tarefas do dia a dia. O agente interage com um board chamado `DIO_Agent` e opera sobre listas como `A FAZER`, `EM ANDAMENTO` e `CONCLUIDO`, facilitando o acompanhamento do fluxo de trabalho.

Atualmente, o agente oferece suporte para:

- adicionar novas tarefas com nome, descricao e data de vencimento
- listar tarefas por status ou retornar todas
- mover cards entre listas do board
- gerar contexto temporal para apoiar a organizacao das atividades do dia

## Tecnologias utilizadas

- Python
- Google ADK
- py-trello
- python-dotenv

## Estrutura do projeto

```text
trello_agent/
|-- README.md
`-- trello_agent/
    `-- taskmanageragent/
        |-- __init__.py
        `-- agent.py
```

## Como funciona

O arquivo principal do projeto e [trello_agent/taskmanageragent/agent.py](/z:/PROJETOS/DIO/trello_agent/trello_agent/taskmanageragent/agent.py). Nele, o agente:

- cria uma conexao com a API do Trello
- busca o board `DIO_Agent`
- localiza as listas do fluxo de trabalho
- cria, lista e movimenta cards

## Configuracao

### 1. Clone o repositorio

```bash
git clone <URL_DO_REPOSITORIO>
cd trello_agent
```

### 2. Crie e ative um ambiente virtual

No Windows:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

No Linux/macOS:

```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Instale as dependencias

```bash
pip install google-adk py-trello python-dotenv
```

Se preferir, voce tambem pode manter um `requirements.txt` com essas dependencias e instalar com:

```bash
pip install -r requirements.txt
```

### 4. Configure as variaveis de ambiente

Crie um arquivo `.env` em `trello_agent/taskmanageragent/.env` com o seguinte formato:

```env
GOOGLE_GENAI_USE_VERTEXAI=0
GOOGLE_API_KEY=sua_google_api_key
TRELLO_API_KEY=sua_trello_api_key
TRELLO_API_SECRET=seu_trello_api_secret
TRELLO_TOKEN=seu_trello_token
```

## Funcoes disponiveis

### `get_temporal_context()`

Retorna a data e hora atual para dar contexto temporal ao agente.

### `adicionar_tarefa(nome_da_task, descricao_da_task, due_date)`

Cria um novo card na lista inicial do board com nome, descricao e data de vencimento.

### `listar_tarefas(status="todas")`

Lista as tarefas do board, permitindo filtrar por status como:

- `todas`
- `a fazer`
- `em andamento`
- `concluido`

### `mudar_status_tarefa(nome_da_task, novo_status)`

Move uma tarefa existente para outra lista do fluxo.

## Exemplo de uso

Exemplo de chamada das funcoes diretamente em Python:

```python
from trello_agent.taskmanageragent.agent import adicionar_tarefa, listar_tarefas, mudar_status_tarefa

adicionar_tarefa(
    nome_da_task="Estudar Python",
    descricao_da_task="Revisar funcoes e estruturas de dados",
    due_date="2026-04-10"
)

print(listar_tarefas("a fazer"))

print(mudar_status_tarefa("Estudar Python", "em andamento"))
```

## Melhorias futuras

- adicionar remocao de tarefas
- melhorar o tratamento de erros quando board ou listas nao existirem
- padronizar melhor os nomes das listas
- criar testes automatizados
- adicionar um `.env.example` para facilitar a configuracao

## Seguranca

Nao publique no GitHub chaves reais da API do Google ou do Trello. O ideal e manter essas credenciais apenas no arquivo `.env`, que deve estar ignorado pelo Git.

## Licenca

Este projeto pode ser utilizado para fins de estudo, aprendizado e evolucao pessoal. Se desejar, voce pode adicionar uma licenca como MIT para uso aberto no GitHub.
