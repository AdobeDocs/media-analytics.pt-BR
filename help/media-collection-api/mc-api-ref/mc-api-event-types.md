---
title: Tipos e descrições de eventos de mídia de transmissão
description: "Quais são os tipos e descrições dos eventos da coleção de mídia? "
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 95%

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

Se você não enviar um `sessionEnd`, uma sessão abandonada sofrerá tempo limite normalmente (se nenhum evento for recebido por 10 minutos ou quando nenhum movimento do indicador de reprodução ocorrer por 30 minutos) e a sessão será excluída pelo back-end.

## sessionComplete

Enviado quando o fim do conteúdo principal é atingido

>[!IMPORTANT]
>
>Você deve consultar os [Esquemas de validação JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) para cada tipo de evento, a fim de verificar os tipos e requisitos corretos dos parâmetros de evento.
