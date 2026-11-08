# Fluxo de interação (versão web)

O usuário diz qual serviço precisa. Pedimos só os dados que aquele serviço
exige e agendamos por ele.

## Canal

- **App web instalável (PWA)** com um assistente em formato de conversa.
- **Notificações:** push no navegador (grátis; no iPhone exige adicionar à tela
  inicial, iOS 16.4+) com **e-mail** de reserva.
- **WhatsApp:** fora do MVP. A API oficial cobra pelas mensagens enviadas fora
  da janela de 24h, que são justamente os avisos do modo caçador. Pode ser
  adicionado depois, só para esses avisos.

## Produtos

| Produto | Preço | O que faz |
|---|---|---|
| **Agendamento** | Gratuito | Triagem, coleta de dados, agendamento da melhor vaga disponível, lembretes e checklist |
| **Modo caçador** | Pago à parte | Monitora desistências e avisa quando surge vaga melhor; **troca só com confirmação do usuário** |

Cobramos pelo **serviço de monitoramento**, nunca "pela vaga". Não reservamos
vagas sem um usuário real com os dados dele e não seguramos vagas em estoque.

## Etapas

1. **Pedido em linguagem natural.** Ex.: "quero renovar meu passaporte, viajo
   dia 20/01". Identificamos o serviço no [catálogo](../catalogo/) e guardamos
   restrições (a data da viagem vira **prazo-limite**).
2. **Triagem.** As perguntas do campo `triagem` do catálogo, que escolhem a
   variante do serviço e os documentos exigidos. Se o serviço puder ser feito
   100% online, avisamos e oferecemos esse caminho em vez do presencial.
3. **Coleta.** Só os campos do serviço. Foto do documento → OCR → usuário
   confirma. Os dados ficam no perfil e são reaproveitados em outros serviços.
4. **Taxa** (quando houver). Geramos a guia e acompanhamos a compensação. O
   agendamento só é liberado depois da compensação, que pode levar um dia útil.
5. **Preferências e consentimento.** Locais aceitos (unidades ou raio), dias e
   horários disponíveis, e aceite explícito: "Autorizo o FuraFila a agendar em
   meu nome" (LGPD).
6. **Agendamento.** Marcamos imediatamente a melhor vaga disponível dentro das
   preferências. O usuário nunca fica sem vaga.
7. **Confirmação e acompanhamento.** Comprovante, evento de calendário (.ics),
   checklist do que levar, lembretes D-3 e D-1. Se o usuário não puder ir,
   cancelamos no site para liberar a vaga.

## Modo caçador (pago)

Oferecido ao fim da etapa 6: "Sua vaga é dia 12/12. Quer que eu procure uma
mais cedo?"

1. O usuário define os **critérios de vaga melhor**: antes de qual data, em
   quais unidades, em quais horários.
2. Pagamento e ativação. Validade até o prazo-limite ou até a data da vaga atual.
3. Monitoramos as desistências respeitando os limites de cada site
   (`cacador.intervalo_minimo_segundos` no catálogo).
4. Encontrou uma vaga dentro dos critérios → **push + e-mail imediatos**:
   > 🎯 Vaga em 28/11 às 10h na PF Lapa (hoje você tem 12/12). Trocar?
   > [Trocar] [Ignorar]
5. **A troca só acontece com a confirmação do usuário.** Como vagas de
   desistência somem em minutos:
   - o aviso tem validade curta e mostra quanto tempo se passou;
   - ao confirmar, verificamos de novo se a vaga existe antes de agir;
   - se a vaga sumiu, avisamos e seguimos caçando, sem mexer na vaga atual.
6. **Ordem da troca:** sempre garantir a nova vaga **antes** de abrir mão da
   atual. Se o site cancela a vaga antiga ao reagendar, só confirmamos quando a
   nova estiver disponível naquele instante (ver
   `reagendamento.cancela_anterior` no catálogo).
7. O caçador encerra quando o usuário aceita uma troca que atende todos os
   critérios, quando ele desliga, ou quando o prazo acaba.

## Estados de um pedido

```
rascunho → triagem → coleta → aguardando_pagamento_taxa → preferencias
        → agendado ──(caçador ativo)──> cacando ⇄ vaga_encontrada(aguardando_usuario)
        → atendido | cancelado | expirado
```

## Resultado da verificação

Ver [verificacao.md](verificacao.md). Em resumo: o passaporte não exige gov.br,
mas tem CAPTCHA e permite só 2 trocas a cada 30 dias; o Poupatempo exige login
gov.br. Isso bloqueia o monitoramento automático do modo caçador nos dois
serviços, e o modelo do caçador precisa ser revisto.
