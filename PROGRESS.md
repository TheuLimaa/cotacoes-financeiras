# Progresso do projeto

Última atualização: 2026-09-29

## O que já fiz

- [x] Criei a estrutura de pastas (`data/raw`, `data/processed`, `notebooks`, `src`)
- [x] Escrevi o `README.md`, `.gitignore` e `requirements.txt`
- [x] Iniciei o repositório com `git init` e publiquei em
      `github.com/TheuLimaa/cotacoes-financeiras`
- [x] Peguei minha chave da API Alpha Vantage e guardei com segurança em
      `src/config.py` (arquivo protegido no `.gitignore`, nunca commitado)
- [x] **Fiz o primeiro ciclo completo de extração e limpeza de dados**, em
      `notebooks/01_extracao.ipynb`:
  - Descobri que `FX_DAILY` (câmbio) virou endpoint pago da API e troquei para
    `TIME_SERIES_DAILY` (ações), que continua gratuito
  - Entendi a estrutura da resposta da Alpha Vantage: um **dicionário** (não uma
    lista) com `"Meta Data"` e `"Time Series (Daily)"`, sendo esse último um
    dicionário-de-dicionários (data → métricas do dia) — um formato diferente do
    Banco Mundial (lista com metadados) e do Banco Central (lista direta de registros)
  - Converti pra tabela com `pd.DataFrame.from_dict(serie, orient="index")`
  - Renomeei as colunas (`1. open` → `abertura`, etc.) com `.rename(columns={...})`
  - Corrigi os tipos: preço/volume de `str` para `float`/`int` com `.astype({...})`;
    índice de data convertido para datetime de verdade com `pd.to_datetime()`
  - Chequei nulos (`isna().sum()`) e duplicatas (`duplicated().sum()`) — nenhum problema
  - Salvei o dado bruto em `data/raw/ibm_daily_raw.json` e o tratado em
    `data/processed/ibm_daily.csv` (mantendo o índice, porque é onde está a data)
  - Commitei e mandei pro GitHub
  - Corrigi um problema em que o notebook tinha sido commitado vazio (esquecimento de
    salvar antes do `git add`) — lição: sempre conferir tamanho/conteúdo do arquivo
    antes de confiar no commit

## Nota

Cheguei a montar aqui uma simulação de API SQL (servidor fictício + extração +
tratamento em SQL) pra praticar o fluxo que uso no trabalho, mas decidi separar isso
num repositório próprio, `tratamento-dados-sql`, já que é um assunto diferente
(SQL puro, sem pandas) do que esse projeto se propõe. Esse projeto aqui continua
focado em Python + pandas + API REST pública.

## Próximo passo

Ainda preciso decidir entre:

1. **Buscar uma segunda tabela** (outra ação, ou `OVERVIEW` com dados da empresa) pra
   praticar merge entre duas tabelas — mesmo padrão que usei no projeto do Banco Mundial
2. **Ir para SQL** — carregar `ibm_daily.csv` num banco SQLite e praticar consultas
3. Ou definir uma direção nova, dependendo do que fizer mais sentido na hora

## Como estou trabalhando nesse projeto

- Escrevo e rodo todo o código eu mesmo; peço ajuda só pra entender conceitos e
  destravar erros — não deixo resolverem por mim.
- Nunca commito `src/config.py` (tem minha chave da API) — sempre confiro com
  `git status` antes de commitar por perto.
- Documentação (README, este arquivo) pode ser escrita com ajuda; código técnico, não.
- Aprendi a sempre conferir a mensagem de erro exata antes de tentar corrigir algo no
  terminal — erro de digitação é comum e a mensagem geralmente já aponta o problema.
