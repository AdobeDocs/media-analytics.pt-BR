---
seo-title: Tipos e descrições de eventos
title: Tipos e descrições de eventos
uuid: bc 4 f 75 a 7-ea 22-47 eb-a 50 d -5 f 41274 c 6 d 41
translation-type: tm+mt
source-git-commit: 69057b2abf7140d52b1897af3dc9d9fd01ca87ad

---


# Tipos e descrições de eventos{#event-types-and-descriptions}

## sessionStart

Sent with the `sessions` call. Quando a resposta é obtida, você extrai a ID da sessão do cabeçalho Localização e a usa para as chamadas de eventos subsequentes ao servidor de coleta.

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). Outros estados a partir dos quais o reprodutor passa para "reproduzindo" incluem "buffering", o usuário retomou de um estado "pausado", o reprodutor recuperou-se de um erro, reprodução automática e assim por diante.

## ping

* **Conteúdo principal -** Deve ser enviado a cada 10 segundos durante a reprodução do conteúdo principal, independentemente de outros eventos de API enviados. O primeiro evento de ping deve ser disparado 10 segundos após o início da reprodução do conteúdo principal.
* **Conteúdo do anúncio-** Deve ser enviado a cada 1 segundo durante o rastreamento do anúncio.

Os eventos de ping *não* devem incluir o mapa `params` no corpo da solicitação.

## Bitratechange

Enviado quando a taxa de bits muda.

## bufferStart

Enviado quando o buffering é iniciado. Não há um tipo de evento `bufferResume`. A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

Enviado quando o usuário pressiona Pausar. Não há um tipo de evento `resume`. A `resume` is inferred when you send a `play` event after a `pauseStart`.

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

Sinaliza um capítulo ignorado

## chapterComplete

Sinaliza a conclusão de um capítulo

## error

Sinaliza um erro.

## sessionEnd

Isso é usado para notificar ao backend do Media Analytics para encerrar imediatamente a sessão quando o usuário abandonou sua exibição do conteúdo e não pode retornar.

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

Enviado quando o fim do conteúdo principal é atingido

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](../../media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

