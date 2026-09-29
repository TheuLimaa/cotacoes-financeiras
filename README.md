# Cotações Financeiras

Projeto de estudo para praticar Python, pandas, SQL e Power BI, extraindo dados
financeiros reais via API REST (Alpha Vantage — cotações de câmbio e ações),
tratando com pandas, e futuramente carregando num banco e num dashboard.

## Fonte de dados

[Alpha Vantage](https://www.alphavantage.co/) — API pública e gratuita de dados
financeiros. Requer uma chave de API gratuita (cadastro rápido, sem cartão de
crédito), enviada como parâmetro `apikey` na própria URL da requisição.

## Estrutura do projeto


cotacoes-financeiras/
├── data/
│   ├── raw/          # dados brutos, exatamente como vieram da API (fora do Git)
│   └── processed/    # dados já tratados, prontos para análise
├── notebooks/        # notebooks Jupyter (extração, limpeza, análise)
├── src/              # código Python reutilizável (ex.: cliente da API)
├── requirements.txt  # bibliotecas necessárias
└── .gitignore


## Como rodar

```powershell
pip install -r requirements.txt
jupyter notebook
