# Mais dinheiro, melhores serviços? Repasses aos municípios do RN

Projeto da 2ª Unidade da disciplina **Ciência de Dados** (IMD1151, UFRN/IMD), 2026.2.

**Membros:** Brenda Gomes, Fernanda Nascimento, Gabriel Borges e Renata Nascimento.

**Pergunta de pesquisa:** o dinheiro que chega às prefeituras do RN (repasses obrigatórios do Estado, convênios e
emendas parlamentares) faz diferença para a população? As prefeituras dependem dele? Para onde vai o dinheiro a mais?
E mais dinheiro significa melhores serviços? Analisamos os **167 municípios**, de **2020 a 2023**, em reais de 2023.

## Principais resultados

- **R$ 10,4 bilhões** chegaram às prefeituras em 4 anos: **85% são repasses obrigatórios**, 9% convênios e 6% emendas.
- A cidade típica recebe cerca de **R$ 740 por habitante por ano**. Pela regra do boxplot, o limite é **R$ 2.400**, e
  **seis cidades passam dele** (cidades em destaque): Guamaré, Galinhos, Parazinho, São Bento do Norte, Pedra Grande e
  Bodó. Cada uma foi comparada com uma **cidade gêmea** (mesma mesorregião e população parecida): de 4 a 20 vezes mais
  dinheiro por habitante.
- **Dependência:** cerca de 90% da receita das prefeituras vem de transferências. Nas cidades gêmeas o FPM é quase
  metade ou mais da receita; nas cidades em destaque, o dinheiro do Estado (ICMS) ocupa o lugar do FPM.
- **Gastos:** de cada R$ 100 gastos a mais pelas cidades em destaque, R$ 32 vão para administração e Câmara, R$ 25 para
  saúde, R$ 20 para educação e R$ 8 para obras e saneamento.
- **Serviços:** sem vantagem clara. A cidade em destaque vai melhor no IDEB, a gêmea vai melhor na água encanada, e os
  demais indicadores (pobreza, esgoto, lixo, mortalidade infantil) ficam divididos.

## Onde está o quê

A versão **definitiva** do projeto é a pasta **[`resultado_final/`](resultado_final/)**. Ela reúne, em ordem, os
notebooks que juntam as fontes de dinheiro, escolhem as cidades em destaque e as cidades gêmeas, comparam dependência,
gastos e indicadores sociais e, por fim, consolidam os resultados. A leitura começa pelo
[`resultado_final/README.md`](resultado_final/README.md), que detalha a ordem dos notebooks, o padrão dos dados e as
regras de junção.

```
resultado_final/
├── README.md         ← comece por aqui
├── notebooks/         01 a 07, nessa ordem
└── saida/             CSVs que os notebooks geram
```

O restante do repositório é histórico do projeto (etapas anteriores à versão final) e dados brutos usados pelos
notebooks:

```
dados/            dados brutos de todas as fontes (SEFAZ, IBGE, MDS, convênios, emendas, SICONFI, INEP, saúde)
notebooks/        notebooks de etapas anteriores (coleta inicial, EDA, outliers, série longa)
saida/            CSVs gerados pelos notebooks da pasta notebooks/
```

## Os notebooks da `resultado_final/`

| # | Notebook | O que faz |
|---|---|---|
| 01 | `01_repasses.ipynb` | Repasses obrigatórios do Estado (ICMS, IPVA, IPI-Exportação e royalties), com população, PIB e CadÚnico |
| 02 | `02_convenios.ipynb` | Convênios federais e estaduais com as prefeituras |
| 03 | `03_emendas.ipynb` | Emendas parlamentares federais pagas às prefeituras (Pix, convênio e outras) |
| 04 | `04_juncao_e_destaques.ipynb` | Junta as três fontes sem contar nada duas vezes e define as cidades em destaque |
| 05 | `05_cidades_gemeas.ipynb` | Escolhe a cidade gêmea de cada cidade em destaque |
| 06 | `06_dependencia_e_gastos.ipynb` | Dependência das transferências, gasto por área e indicadores de serviços; traz os gráficos usados na apresentação |
| 07 | `07_resultado_final_consolidado.ipynb` | Síntese executiva: reúne a dependência, o gasto, o comparativo par a par e a visão dos 167 municípios, com as conclusões em um só lugar |

Os notebooks 01 a 06 são a base das análises, e a **apresentação e o relatório usam os números do notebook 06**. O
notebook 07 é uma síntese consolidada feita a partir das mesmas bases e **trabalha com 7 pares** (inclui a Serra do
Mel, que fica logo abaixo do limite de destaque); por isso alguns valores dele podem diferir um pouco dos do 06, que usa
os 6 pares da apresentação em seus gráficos novos.

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

Rode os notebooks da `resultado_final/` **na ordem** (01 → 07): cada um usa o CSV gerado pelo anterior, salvo em
`resultado_final/saida/`. Eles lêem os dados brutos de `dados/` (pelo GitHub ou por uma cópia local, se já tiver
clonado o repositório).

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
| `07_resultado_final_consolidado.ipynb` | Bases já tratadas nos notebooks anteriores (SICONFI, indicadores sociais e CSVs da `resultado_final/saida/`) | Nenhuma coleta nova: lê as cópias em `dados/` e `resultado_final/saida/` |

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
