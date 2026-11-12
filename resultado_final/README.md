# Resultado final

Versão definitiva do projeto **"Para onde vai o dinheiro do Estado nos municípios do RN?"**.
Os notebooks devem ser rodados **na ordem**, porque cada um usa o CSV gerado pelo anterior.

## Etapas

| # | Notebook | O que faz | Gera (em `resultado_final/saida/`) |
|---|---|---|---|
| 01 | `01_repasses.ipynb` | Repasses obrigatórios do Estado (cota-parte de ICMS, IPVA, IPI-exportação e royalties), com população, PIB e CadÚnico | `01_repasses_municipio_ano.csv`, `01_repasses_municipios_2020_2023.csv`, `01_base_municipios_2020_2023.csv` |
| 02 | `02_convenios.ipynb` | Convênios federais e estaduais com as prefeituras, sem os anulados e corrigidos pelo IPCA | `02_convenios_municipio_ano.csv`, `02_convenios_municipios_2020_2023.csv` |
| 03 | `03_emendas.ipynb` | Emendas parlamentares (Pix e as demais), marcando quais chegaram por convênio | `03_emendas_municipio_ano.csv`, `03_emendas_municipios_2020_2023.csv` |
| 04 | `04_juncao_e_destaques.ipynb` | Junta as três fontes sem contar nada duas vezes e define as cidades em destaque (outliers) | `04_base_unificada_2020_2023.csv`, `04_cidades_destaque.csv` |
| 05 | `05_cidades_gemeas.ipynb` | Escolhe a cidade gêmea de cada cidade em destaque | `05_pares_gemeos.csv` |
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

- dos convênios federais, somar só `fed_sem_emenda_valor`;
- das emendas, somar todas (Pix e as que vieram por convênio).
