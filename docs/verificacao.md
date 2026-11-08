# Verificação nos sites oficiais (08/11/2026)

## Passaporte (Polícia Federal)

Fontes: [página do passaporte](https://www.gov.br/pf/pt-br/assuntos/passaporte),
[documentação](https://www.gov.br/pf/pt-br/assuntos/passaporte/links/lista-geral),
[dúvidas frequentes](https://www.gov.br/pf/pt-br/assuntos/passaporte/duvidas),
[reagendar](https://www.gov.br/pf/pt-br/assuntos/passaporte/documentacao/formulario/pagar-taxa/agendamento/reagendar).

| Item | Resultado |
|---|---|
| Login gov.br | **Não exige.** O sistema (SINPA, `servicos.pf.gov.br`) pede CPF e data de nascimento |
| CAPTCHA | **Sim.** CAPTCHA de imagem no reagendamento; desafio antibot da Cloudflare na página de agendamento |
| Taxa | R$ 257,25 comum; R$ 334,42 com urgência; R$ 514,50 com perda ou extravio. Furto ou roubo com BO paga só a taxa comum |
| Agendar após pagar | Pix: logo após a compensação. Boleto: 72 horas úteis |
| Validade da taxa | 5 anos |
| Agendamentos por CPF | **1.** Um novo agendamento exige cancelar o anterior |
| Reagendamento | **No máximo 2 a cada 30 dias**, por função própria ("Reagendar") |
| Retirada | No mesmo posto, em até 90 dias, ou o passaporte é cancelado sem reembolso |
| Intermediários | A FAQ diz que "não é necessário pagar por assessoria" e que o pedido deve ser feito "exclusivamente no site da Polícia Federal" |

Não confirmado: se "Reagendar" troca a vaga sem cancelar a anterior antes;
penalidade por falta; tolerância de atraso.

## CIN (Poupatempo SP)

Fontes: [CIN 1ª via](https://www.poupatempo.sp.gov.br/carta/D97C3844-A2D9-4C9E-B364-CB4FEB26A1FB),
[CIN 2ª via](https://www.poupatempo.sp.gov.br/carta/4FC0FEE9-9E3F-4220-8A73-9C49BFDD7288).

| Item | Resultado |
|---|---|
| Login gov.br | **Exige.** O sistema de agendamento responde "acesso negado" sem sessão, e o portal usa "Entrar com o gov.br". Nível de conta não confirmado |
| Agendamento | Obrigatório, pessoal e intransferível. Site, app Poupatempo SP.GOV.BR, WhatsApp ou totem |
| Taxa | 1ª via gratuita; 2ª via R$ 57,63 (+ R$ 9,09 se entregue pelos Correios); Pix ou débito; há isenções |
| Documentos | Certidão do estado civil atual (original e cópia simples) e CPF |
| Prazo de emissão | Até 26 dias úteis. Para viagem ao Mercosul antes disso, a orientação é a identidade provisória |

Não confirmado: regras de reagendamento, limite de trocas, penalidade por
falta, CAPTCHA (fica atrás do login). A FAQ do Poupatempo bloqueou o acesso
automatizado (HTTP 403).

## Impacto no produto

1. **Modo caçador no passaporte.** Para ver vagas é preciso passar por CAPTCHA
   e desafio antibot. Não vamos contorná-los (resolução automática ou serviços
   de quebra de CAPTCHA), então **não dá para monitorar desistências
   automaticamente**. Além disso, só 2 trocas são permitidas a cada 30 dias.
2. **Modo caçador no Poupatempo.** Consultar vagas exige a sessão gov.br do
   usuário. Guardar a senha dele está fora de cogitação; manter a sessão dele
   ativa em nossos servidores também é delicado (LGPD e termos do gov.br).
3. **Agendamento assistido continua viável nos dois.** Nós preparamos tudo
   (triagem, dados, documentos, taxa) e o usuário conclui no site oficial: no
   passaporte, ele resolve o CAPTCHA; no Poupatempo, ele faz o login gov.br.
4. **Próxima verificação:** percorrer os fluxos com um protocolo real, com o
   próprio usuário, para mapear as telas, confirmar se "Reagendar" é uma troca
   atômica e anotar as regras que só aparecem dentro do sistema.
