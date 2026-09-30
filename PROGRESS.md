# Progresso do projeto

Última atualização: 2026-09-29

## O que já foi feito

- [x] Estrutura de pastas criada (`data/raw`, `data/processed`, `notebooks`, `src`)
- [x] `README.md`, `.gitignore`, `requirements.txt` criados
- [x] `git init` + repositório publicado em `github.com/TheuLimaa/cotacoes-financeiras`
- [x] Chave da API Alpha Vantage guardada com segurança em `src/config.py` (gitignored,
      confirmado que nunca foi commitada)
- [x] **Ciclo completo de extração e limpeza da primeira tabela**, em
      `notebooks/01_extracao.ipynb`:
  - Descoberto que `FX_DAILY` (câmbio) virou endpoint pago — trocado para
    `TIME_SERIES_DAILY` (ações), que continua gratuito
  - Entendida a estrutura da resposta da Alpha Vantage: um **dicionário** (não lista)
    com `"Meta Data"` e `"Time Series (Daily)"`, sendo esse último um
    dicionário-de-dicionários (data → métricas do dia), diferente do formato do Banco
    Mundial (lista) e do Banco Central (lista direta)
  - Convertido com `pd.DataFrame.from_dict(serie, orient="index")`
  - Colunas renomeadas (`1. open` → `abertura`, etc.) com `.rename(columns={...})`
  - Tipos corrigidos: colunas de preço/volume de `str` para `float`/`int` com
    `.astype({...})`; índice de data convertido para datetime de verdade com
    `pd.to_datetime()`
  - Checado nulos (`isna().sum()`) e duplicatas (`duplicated().sum()`) — nenhum problema
  - Dado bruto salvo em `data/raw/ibm_daily_raw.json`, dado tratado salvo em
    `data/processed/ibm_daily.csv` (mantendo o índice, pois é onde mora a data)
  - Commitado e enviado ao GitHub

## Próximo passo (quando retomar)

O usuário escolheu **parar por hoje** depois de fechar esse primeiro ciclo. As opções
que ficaram na mesa para a próxima sessão:

1. **Buscar uma segunda tabela** (outra ação, ou `OVERVIEW` com dados da empresa) para
   praticar merge entre duas tabelas — mesmo padrão do projeto do Banco Mundial
2. **Ir para SQL** — carregar `ibm_daily.csv` num banco SQLite e praticar consultas
3. Ou definir uma direção nova, dependendo do que fizer mais sentido na hora

Perguntar ao usuário qual dessas prefere ao retomar.

## Combinados do projeto

- O usuário escreve e roda o código; o assistente só explica e guia (não resolve por
  ele).
- Nunca commitar `src/config.py` (contém a chave da API) — sempre confirmar com
  `git status` antes de commitar quando mexer perto dele.
- Documentação (README, este PROGRESS.md) pode ser escrita pelo assistente; código
  técnico, não.
- Erros de digitação em comandos do terminal são comuns (dictation/transcrição) — vale
  sempre conferir a mensagem de erro exata antes de sugerir a correção.
