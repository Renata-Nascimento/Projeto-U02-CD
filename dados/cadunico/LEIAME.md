# CadÚnico — pessoas inscritas por município (RN)

**Fonte:** Ministério do Desenvolvimento e Assistência Social, Família e Combate à Fome (MDS), API pública VIS DATA (MI Social): https://aplicacoes.mds.gov.br/sagi/servicos/misocial

**Arquivo:** `cadunico_dezembro_rn.csv`, posição de dezembro de cada ano, para os 167 municípios do RN.

| Coluna | Descrição |
|---|---|
| `cod_ibge6` | Código IBGE do município com 6 dígitos (sem o dígito verificador), padrão usado pelo MDS |
| `ano` | Ano de referência (dezembro) |
| `cad_familias` | Famílias inscritas no CadÚnico |
| `cad_pessoas` | Pessoas inscritas no CadÚnico |
| `cad_baixa_renda` | Pessoas com renda familiar per capita de até ½ salário mínimo |

## ⚠️ Dados incompletos

Este arquivo cobre apenas **dezembro de 2020 a 2025**. Ele foi baixado em 13/10/2026, antes de a API do MDS sair do ar.

**Observação de 26/10/2026:** a API está fora do ar desde 21/10/2026. Ao acessá-la, o MDS exibe o aviso "Serviço temporariamente indisponível", por manutenção preventiva de segurança, sem previsão de retorno. Por isso não foi possível buscar os anos anteriores a 2020 para a série longa (2004–2025).

O notebook `05_b_indicadores` tenta a API primeiro e só usa este arquivo se ela não responder. Quando a API voltar, basta rodar o notebook de novo para obter todos os anos disponíveis e substituir este arquivo pela versão atualizada.
