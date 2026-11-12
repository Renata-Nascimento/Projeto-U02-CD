# Emendas parlamentares

## Arquivos usados no `resultado_final/notebooks/03_emendas.ipynb`

| Arquivo | Fonte | Conteúdo |
|---|---|---|
| `emendas_por_favorecido_rn.csv` | Portal da Transparência federal, arquivo `EmendasParlamentares_PorFavorecido.csv` | Quanto cada favorecido do RN recebeu de cada emenda, mês a mês (2014 a 2026) |
| `emendas_por_localidade_rn.csv` | Portal da Transparência federal, arquivo `EmendasParlamentares.csv` | Valor empenhado, liquidado e pago de cada emenda por local de aplicação, só UF = RN |
| `emendas_convenios_rn_portal.csv` | Portal da Transparência federal, arquivo `EmendasParlamentares_Convenios.csv` | Emendas que viraram convênio, só localidades do RN |
| `transferegov_pix_rn.csv` | API do Transferegov (transferências especiais) | Planos de ação do Pix no RN, com o valor pago por ano (ordens bancárias) |

Os três primeiros são o recorte do RN do arquivo nacional
[EmendasParlamentares.zip](https://portaldatransparencia.gov.br/download-de-dados/emendas-parlamentares), baixado em
12/11/2026 (dados da CGU de 10/11/2026). O arquivo nacional tem cerca de 250 MB e não cabe no GitHub. Para atualizar,
baixe o zip de novo pelo navegador e filtre o RN: `UF Favorecido = RN`, `UF = RIO GRANDE DO NORTE` e localidade
terminando em `- RN`, respectivamente.

## Outros arquivos desta pasta (análises anteriores)

`EmendasParlamentares_Convenios.csv` (nacional), `convenio.csv`, `emendas_convenios_rn.csv`, `emendas_pix_rn.csv`,
`convenios_rn_tratados_2020_2023.csv` e os notebooks desta pasta são de etapas anteriores do projeto. O notebook 02 do
`resultado_final` usa `convenio.csv` e `EmendasParlamentares_Convenios.csv`.
