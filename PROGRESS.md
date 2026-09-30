# Progresso do projeto

Última atualização: 2026-09-28

## O que já foi feito

- [x] Estrutura de pastas criada (`data/raw`, `data/processed`, `notebooks`, `src`)
- [x] `README.md`, `.gitignore`, `requirements.txt` criados
- [x] `git init` + primeiro commit + push para
      `github.com/TheuLimaa/cotacoes-financeiras`
- [x] Chave da API Alpha Vantage obtida e guardada com segurança em `src/config.py`
      (arquivo no `.gitignore`, confirmado que nunca foi commitado)
- [ ] **Notebook `notebooks/01_extracao.ipynb` em andamento** — primeira célula escrita,
      ainda não confirmado se rodou com sucesso

## Exatamente onde parar / retomar

A célula que está no notebook (ainda não testada):

```python
import sys
from pathlib import Path

sys.path.insert(0, str(Path.cwd().parent))

from src.config import API_KEY
import requests

url = f"https://www.alphavantage.co/query?function=FX_DAILY&from_symbol=USD&to_symbol=BRL&apikey={API_KEY}"
resposta = requests.get(url)
resposta.json()
```

**Próximo passo:** rodar essa célula e ver o resultado. Se dar erro tipo
`"Invalid API call"`, colar a mensagem exata para debugar juntos. Se funcionar, os
próximos passos (na mesma lógica do projeto do Banco Mundial) são:
1. Separar a parte do JSON que interessa (a Alpha Vantage também costuma vir com um
   "envelope" de metadados + os dados de verdade — precisa olhar a estrutura crua
   primeiro, igual fizemos antes)
2. Transformar em DataFrame com pandas
3. Tratar tipos (datas, números que vêm como texto)
4. Salvar em `data/raw/`

## Combinados do projeto

- O usuário escreve e roda o código; o assistente só explica e guia (não resolve por
  ele) — mesma regra do projeto do Banco Mundial.
- Nunca commitar `src/config.py` (contém a chave da API).
- Documentação (README, este PROGRESS.md) pode ser escrita pelo assistente; código
  técnico, não.
