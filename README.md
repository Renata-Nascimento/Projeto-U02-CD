# Para onde vai o dinheiro do Estado nos municípios do RN?

Projeto da 2ª Unidade da disciplina **Ciência de Dados** (IMD/UFRN).

**Membros:** Brenda Gomes, Fernanda Nascimento, Gabriel Borges e Renata Nascimento.

**Pergunta de pesquisa:** o Governo do RN repassa aos 167 municípios parte dos impostos que arrecada (ICMS, IPVA,
IPI-Exportação e royalties), além de convênios e emendas parlamentares federais. Essa distribuição reduz ou reforça as
desigualdades entre os municípios? O dinheiro a mais, quando existe, aparece em melhores resultados sociais?

## Onde está o quê

A versão **definitiva** do projeto é a pasta **[`resultado_final/`](resultado_final/)**. Ela reúne, em ordem, os
notebooks que juntam as quatro fontes de dinheiro (repasses, convênios, emendas e a base unificada), escolhem as
cidades em destaque e as cidades gêmeas, e comparam dependência, gastos e indicadores sociais entre elas. A leitura
começa pelo [`resultado_final/README.md`](resultado_final/README.md), que detalha a ordem dos notebooks, o padrão dos
dados e as regras de junção.

```
resultado_final/
├── README.md         ← comece por aqui
├── notebooks/         01 a 06, nessa ordem
└── saida/             CSVs que os notebooks geram
```

O restante do repositório é histórico do projeto (etapas anteriores à versão final) e dados brutos usados pelos
notebooks:

```
dados/            dados brutos de todas as fontes (SEFAZ, IBGE, MDS, convênios, emendas, SICONFI, INEP, saúde)
notebooks/        notebooks de etapas anteriores (coleta inicial, EDA, outliers, série longa)
saida/            CSVs gerados pelos notebooks da pasta notebooks/
```

## Como executar

Os notebooks rodam no **Google Colab**, sem precisar instalar nada: cada um tem o link "Abrir no Colab" na primeira
célula e baixa os dados direto do GitHub (`raw.githubusercontent.com`). É o jeito mais simples e o que o grupo usa no
dia a dia.

Para rodar localmente (Jupyter, VS Code, etc.):

```bash
git clone https://github.com/Renata-Nascimento/Projeto-U02-CD.git
cd Projeto-U02-CD
pip install -r requirements.txt
jupyter notebook resultado_final/notebooks/01_repasses.ipynb
```

Rode os notebooks da `resultado_final/` **na ordem** (01 → 06): cada um usa o CSV gerado pelo anterior, salvo em
`resultado_final/saida/`. Todos executam do início ao fim sem erro, lendo os dados brutos de `dados/` (pelo GitHub ou
por uma cópia local, se já tiver clonado o repositório).

## Coleta dos dados

Não há um único script de coleta: cada notebook da `resultado_final/` baixa e trata os dados da sua própria fonte, com
um plano B caso a API correspondente não responda (fica então a cópia salva em `dados/`, já tratada):

| Notebook | Fonte dos dados | Como é coletado |
|---|---|---|
| `01_repasses.ipynb` | SEFAZ/RN (planilhas `.xls` em `dados/sefaz/`), IBGE (API SIDRA) e MDS (API do CadÚnico) | Direto nas APIs; cópias em `dados/ibge/` e `dados/cadunico/` |
| `02_convenios.ipynb` | Portal da Transparência federal e Controladoria-Geral do RN | Arquivos exportados manualmente (os sites não têm API aberta), em `dados/emendas/` e `dados/convenios/` |
| `03_emendas.ipynb` | Portal da Transparência federal (emendas) e API do Transferegov (Pix) | Arquivo exportado (`dados/emendas/`) + API pública, com plano B na cópia salva |
| `04_juncao_e_destaques.ipynb` | Saídas dos notebooks 01 a 03 | Nenhuma coleta nova: só junta |
| `05_cidades_gemeas.ipynb` | Saída do notebook 04 + Censo 2022 (`dados/ibge/`) | Nenhuma coleta nova |
| `06_dependencia_e_gastos.ipynb` | SICONFI (API do Tesouro Nacional), Censo 2010/2022, IDEB (INEP) e mortalidade infantil (DATASUS) | API do SICONFI (cópia em `dados/siconfi/`); demais já em `dados/` |

Os detalhes de cada fonte, inclusive os links oficiais e o que cada arquivo contém, estão nos `LEIAME.md` de cada
subpasta de `dados/` e na introdução de cada notebook.

## Dependências

A lista está em [`requirements.txt`](requirements.txt). As principais bibliotecas usadas nos notebooks:

| Biblioteca | Para que serve |
|---|---|
| `pandas`, `numpy` | Manipulação e análise dos dados |
| `matplotlib`, `seaborn` | Gráficos |
| `scipy` | Estatística (correlação, regressão, outliers) |
| `requests` | Chamadas às APIs (IBGE, MDS, SICONFI, Transferegov) |
| `openpyxl`, `xlrd` | Leitura das planilhas `.xls`/`.xlsx` da SEFAZ |

No Colab todas já vêm instaladas por padrão.
