# Catálogo de serviços

Um arquivo YAML por serviço. O formulário do assistente é gerado a partir dele.

| Campo | Significado |
|---|---|
| `id`, `nome`, `esfera`, `orgao` | Identificação do serviço |
| `tier` | `A` site público sem login gov.br · `B` exige gov.br · `C` só telefone/presencial |
| `exige_login_govbr` | `true`, `false` ou `a_verificar` |
| `triagem` | Perguntas que escolhem a `variante` e mudam os documentos/campos |
| `variantes` | Versões do serviço (ex.: 1ª via, renovação) com documentos próprios |
| `campos` | Dados a coletar: `id`, `rotulo`, `tipo`, `obrigatorio`, `origem_ocr` |
| `documentos_atendimento` | Checklist do que levar no dia |
| `taxa` | Valor e forma de pagamento, quando houver |
| `reagendamento` | Regras de troca de horário (usadas pelo modo caçador) |
| `cacador` | Se o modo caçador está disponível e o intervalo mínimo entre consultas |

Valores marcados `a_verificar` foram escritos de memória e **devem ser
confirmados no site oficial** antes de ir para produção.
