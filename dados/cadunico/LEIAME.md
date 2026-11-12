# CadÚnico — pessoas inscritas por município (RN)

**Fonte:** Ministério do Desenvolvimento e Assistência Social, Família e Combate à Fome (MDS), API pública MI Social:
https://dadosabertos.mds.gov.br/misocial/ (o mesmo endereço usado pelo
[conjunto de dados do CadÚnico no dados.gov.br](https://dados.gov.br/dados/conjuntos-dados/familias-por-faixa-de-renda-com-cadastro-atualizado-no-cadastro-unico)).

**Arquivo:** `cadunico_dezembro_rn.csv`, posição de **dezembro de 2012 a 2025**, para os 167 municípios do RN
(2.338 linhas, sem valores faltando).

| Coluna | Descrição |
|---|---|
| `cod_ibge6` | Código IBGE do município com 6 dígitos (sem o dígito verificador), padrão usado pelo MDS |
| `ano` | Ano de referência (dezembro) |
| `cad_familias` | Famílias inscritas no CadÚnico |
| `cad_pessoas` | Pessoas inscritas no CadÚnico |
| `cad_baixa_renda` | Pessoas com renda familiar per capita de até ½ salário mínimo |

## Histórico

- **13/10/2026:** primeira versão, com dezembro de 2020 a 2025, baixada de `aplicacoes.mds.gov.br/sagi/servicos/misocial`.
- **21/10/2026:** esse endereço saiu do ar ("manutenção preventiva de segurança"). Hoje ele redireciona para a página de
  avisos do MDS.
- **12/11/2026:** os dados voltaram no endereço novo `dadosabertos.mds.gov.br/misocial/`. O arquivo foi baixado de novo,
  agora de 2012 a 2025. Os anos de 2020 a 2025 são idênticos aos da primeira versão.

**Anos anteriores a 2012:** a API devolve os municípios de 2004 a 2011, mas sem nenhum valor. O MDS não publica esses
anos nessa API.

Os notebooks `01_coleta`, `05_b_indicadores` e `resultado_final/notebooks/01_repasses` tentam a API primeiro e só usam
este arquivo se ela não responder.
