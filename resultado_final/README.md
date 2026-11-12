# Resultado final

Versão definitiva do projeto **"Para onde vai o dinheiro do Estado nos municípios do RN?"**.
Os notebooks devem ser rodados **na ordem**, porque cada um usa o CSV gerado pelo anterior.

## Etapas

| # | Notebook | O que faz | Gera (em `resultado_final/saida/`) |
|---|---|---|---|
| 01 | `01_repasses.ipynb` | Repasses obrigatórios do Estado (cota-parte de ICMS, IPVA, IPI-exportação e royalties), com população, PIB e CadÚnico | `01_repasses_municipio_ano.csv`, `01_repasses_municipios_2020_2023.csv`, `01_base_municipios_2020_2023.csv` |
| 02 | `02_convenios.ipynb` | Convênios federais e estaduais com as prefeituras, sem os anulados e corrigidos pelo IPCA | `02_convenios_municipio_ano.csv`, `02_convenios_municipios_2020_2023.csv` |
| 03 | `03_emendas.ipynb` | Emendas parlamentares federais pagas às prefeituras (Pix, convênio e outras), pelo valor recebido | `03_emendas_municipio_ano.csv`, `03_emendas_municipios_2020_2023.csv` |
| 04 | `04_juncao_e_destaques.ipynb` | Junta as três fontes sem contar nada duas vezes nem perder nada, define as cidades em destaque e mostra o ano a ano de cada cidade | `04_base_unificada_2020_2023.csv`, `04_base_unificada_municipio_ano.csv`, `04_cidades_destaque.csv` |
| 05 | `05_cidades_gemeas.ipynb` | Escolhe a cidade gêmea de cada cidade em destaque: mesma mesorregião e população parecida (baixa renda entra só como comparação) | `05_pares_gemeos.csv` |
| 06 | `06_dependencia_e_gastos.ipynb` | Dependência das transferências, como o dinheiro é gasto e a comparação entre cada destaque e sua gêmea | gráficos (aparecem no próprio notebook executado) |

## Pastas

```
dados/                  dados brutos de todas as fontes (pasta da raiz do repositório, compartilhada)
resultado_final/
├── README.md           este arquivo
├── notebooks/          os notebooks acima
└── saida/              os CSVs que os notebooks geram (começam com o número do notebook)
```

Os dados brutos continuam na pasta `dados/` da raiz para não ter duas cópias do mesmo arquivo.
Dentro de `resultado_final/` fica só o que os notebooks **produzem**. Nenhum notebook desta pasta lê a pasta `saida/`
da raiz: tudo o que eles usam vem de `dados/` ou de `resultado_final/saida/`.

O `01_repasses` reaproveita o código do `notebooks/01_coleta.ipynb` (CP1) e gera exatamente os mesmos valores.

## Padrão dos CSVs de cada fonte (01, 02 e 03)

Para a junção do notebook 04 funcionar direto, os CSVs `_2020_2023` seguem o mesmo padrão:

| Regra | Como fica |
|---|---|
| Chave do município | `cod_ibge` (7 dígitos) e `municipio` (nome oficial do IBGE, ex.: `Assú`) |
| Linhas | Os 167 municípios, inclusive quem recebeu zero |
| Período | Soma de 2020 a 2023 no arquivo `_2020_2023`; ano a ano no arquivo `_municipio_ano` |
| Valores | Colunas terminadas em `_valor`: em reais de 2023 (corrigidos pela média anual do IPCA) |
| Por habitante | Colunas terminadas em `_pc_ano`: valor ÷ população (Censo 2022, a mesma do notebook 01) ÷ 4 anos |
| Posição | `posicao_<fonte>`: posição no valor por habitante (1 = quem mais recebe) |

**Atenção:** no `01_base_municipios_2020_2023.csv` (uma linha por município e ano), as colunas `rep_*` estão sem
correção pela inflação. Para comparar anos, use `rep_total_real` ou multiplique por `fator_ipca`.

## Cuidado na junção: não contar a mesma emenda duas vezes

A emenda diz **quem decidiu** mandar o dinheiro (um parlamentar). O convênio é **o caminho** que o dinheiro faz.
Uma emenda paga por convênio aparece nas duas bases. Por isso, no notebook 04:

- **repasses:** `rep_total_valor` do `01_repasses_municipios_2020_2023.csv`;
- **convênios:** `total_valor` do `02_convenios_municipios_2020_2023.csv` (federais e estaduais, com e sem emenda);
- **emendas:** só `sem_convenio_valor` do `03_emendas_municipios_2020_2023.csv` (Pix + outros pagamentos diretos).
  A parte das emendas que veio por convênio (`convenio_valor`) já está dentro dos convênios do 02;
- **emendas em convênios anteriores a 2020:** pagamentos de emenda feitos em 2020–2023 em convênios que começaram antes
  de 2020. Eles não estão no 02 (fora do recorte) nem no `sem_convenio_valor`, e o notebook 04 os recupera pelo número
  do convênio (cerca de R$ 295 milhões).

A conta pronta está no `04_base_unificada_2020_2023.csv` (coluna `total_valor`).

**Saúde fundo a fundo:** fica só como informação no 03 e **não entra na junção**. De 2020 a 2023 o Portal não
identifica o município dessa emenda; ela só aparece por município a partir de 2024, fora do período do projeto.

**Datas diferentes entre 02 e 03:** o 02 conta cada convênio no ano em que começou, e o 03 conta cada pagamento no ano
em que chegou. Por isso a junção cruza os dois pelo número do convênio: o que já está no 02 não é somado de novo, e o
que ficaria de fora dos dois (por exemplo, emenda paga em 2021 num convênio que começou em 2018) é recuperado.
