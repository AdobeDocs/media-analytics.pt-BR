---
title: Tipos e descrições de eventos de mídia de streaming
description: 'Quais são os tipos e as descrições de evento da Coleção de mídia? '
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 79%

---

# Tipos e descrições de eventos{#event-types-and-descriptions}

## sessionStart

Enviado com a chamada `sessions`. Quando a resposta é obtida, você extrai a ID da sessão do cabeçalho Localização e a usa para as chamadas de eventos subsequentes ao servidor de coleta.

## play

Enviado quando o reprodutor muda o estado para &quot;reproduzindo&quot; a partir de outro estado (ou seja, o retorno de chamada `on('Playing')` é acionado pelo reprodutor). Outros estados a partir dos quais o reprodutor passa para &quot;reproduzindo&quot; incluem &quot;buffering&quot;, o usuário retomou de um estado &quot;pausado&quot;, o reprodutor recuperou-se de um erro, reprodução automática e assim por diante.

## ping

* **Conteúdo principal -** Deve ser enviado a cada 10 segundos durante a reprodução do conteúdo principal, independentemente de outros eventos de API enviados. O primeiro evento ping deve disparar 10 segundos após o início da reprodução do conteúdo principal.
* **Conteúdo do anúncio -** Deve ser enviado a cada 1 segundo durante o rastreamento do anúncio.

Os eventos de ping *não* devem incluir o mapa `params` no corpo da solicitação.

## bitrateChange

Enviado quando a taxa de bits é alterada.

## bufferStart

Enviado quando o buffering é iniciado. Não há um tipo de evento `bufferResume`. Um `bufferResume` é inferido quando você envia um evento `play` após `bufferStart`.

## pauseStart

Enviado quando o usuário pressiona Pausar. Não há um tipo de evento `resume`. Um `resume` é inferido quando você envia um evento de `play` após um `pauseStart`.

## adBreakStart

Sinaliza o início de um ad break

## adStart

Sinaliza o início de um anúncio

## adComplete

Sinaliza a conclusão de um ad break

## adSkip

Sinaliza um anúncio ignorado

## adBreakComplete

Sinaliza a conclusão de um ad break

## chapterStart

Sinaliza o início de um segmento de capítulo

## chapterSkip

Sinaliza que um capítulo foi ignorado

## chapterComplete

Sinaliza a conclusão de um capítulo

## error

Sinaliza que ocorreu um erro.

## sessionEnd

É usado para notificar o back-end do Media Analytics para encerrar imediatamente a sessão quando o usuário abandona a visualização do conteúdo e é improvável que retorne.

Se um `sessionEnd` não for enviado, uma sessão abandonada irá [expirar normalmente](../mc-api-impl/mc-api-timeout.md) (seja após nenhum evento ser recebido por 10 minutos ou quando nenhum movimento do indicador de reprodução ocorrer por 30 minutos). Além disso, todas as chamadas de mídia subsequentes feitas com essa ID de sessão serão descartadas.

## sessionComplete

Enviado quando o fim do conteúdo principal é atingido

>[!IMPORTANT]
>
>Você deve consultar os [Esquemas de validação JSON](mc-api-json-validation.md) para cada tipo de evento, a fim de verificar os tipos e requisitos corretos dos parâmetros de evento.

## stateStart

Sinaliza o início do rastreamento do estado do player.

Para obter mais informações, consulte [Implementação e relatórios](/help/use-cases/player-state-tracking/implementation-and-reporting.md).

## stateEnd

Sinaliza o fim do rastreamento do estado do player.

Para obter mais informações, consulte [Implementação e relatórios](/help/use-cases/player-state-tracking/implementation-and-reporting.md).
