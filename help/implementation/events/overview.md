---
title: Visão geral dos eventos de mídia de transmissão
description: Saiba mais sobre os tipos de evento de mídia e a ordem em que eles devem ser enviados.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 4%

---


# Eventos de mídia de transmissão

O rastreamento de streaming de mídia funciona enviando uma sequência de chamadas de evento, cada uma representando uma transição de estado do player, para um endpoint de coleção de dados da Adobe. Todo evento pertence a uma sessão ativa que começa com uma chamada [sessionStart](session/session-start.md) e termina com [sessionComplete](session/session-complete.md) ou [sessionEnd](session/session-end.md).

## Fluxo de trabalho do evento

A lista ordenada a seguir mostra a sequência de eventos necessária para uma reprodução típica de VOD com um anúncio precedente e um capítulo:

1. **[Início da sessão](session/session-start.md)**: sempre o primeiro evento; cria a sessão e retorna uma ID de sessão
2. **[Início de quebra de anúncio](ads/ad-break-start.md)**: obrigatório antes de qualquer evento de anúncio
3. **[Início do anúncio](ads/ad-start.md)** → **[Anúncio concluído](ads/ad-complete.md)** (ou **[Ignorar anúncio](ads/ad-skip.md)**)
4. **[Pausa do anúncio concluída](ads/ad-break-complete.md)**: obrigatória depois de todos os anúncios na pausa
5. **[Reproduzir](playback/play.md)**: sinaliza que a reprodução do conteúdo começa ou continua
6. **[Início do capítulo](chapters/chapter-start.md)**: opcional; marca o início de um capítulo
7. **[Ping](playback/ping.md)**: Enviado a cada 10 segundos durante o conteúdo principal, a cada 1 segundo durante os anúncios
8. **[Capítulo concluído](chapters/chapter-complete.md)**: opcional; marca o fim de um capítulo
9. **[Início da pausa](playback/pause-start.md)** → **[Reproduzir](playback/play.md)** (continuar): para qualquer pausa
10. **[Início do buffer](playback/buffer-start.md)** → **[Reproduzir](playback/play.md)** (retomar): para qualquer buffer
11. **[Sessão concluída](session/session-complete.md)**: quando o visualizador atinge o fim do conteúdo

Use [Fim de sessão](session/session-end.md) em vez de Sessão concluída se o visualizador abandonar a sessão antes de atingir o fim do conteúdo.

## Ciclo de vida da sessão

Uma sessão expira automaticamente se qualquer uma das seguintes condições for atendida:

* Nenhum evento é recebido por **10 minutos**
* Nenhum movimento do indicador de reprodução por **30 minutos**

## Referência de evento

| Evento | Categoria | Métrica associada |
| --- | --- | --- |
| [Início da sessão](session/session-start.md) | Sessão | [Início da mídia](/help/reporting/metrics/media-starts.md) |
| [Sessão concluída](session/session-complete.md) | Sessão | [Conteúdo concluído](/help/reporting/metrics/content-completes.md) |
| [Fim da sessão](session/session-end.md) | Sessão | — |
| [Reproduzir](playback/play.md) | Reprodução | [Início do conteúdo](/help/reporting/metrics/content-starts.md) |
| [Início da pausa](playback/pause-start.md) | Reprodução | [Pausar eventos](/help/reporting/metrics/pause-events.md) |
| [Início do buffer](playback/buffer-start.md) | Reprodução | [Eventos de buffer](/help/reporting/metrics/buffer-events.md) |
| [Alteração na taxa de bits](playback/bitrate-change.md) | Reprodução | [Alterações na taxa de bits](/help/reporting/metrics/bitrate-changes.md) |
| [Ping](playback/ping.md) | Reprodução | — |
| [Início de quebra de anúncio](ads/ad-break-start.md) | Anúncios | — |
| [Início do anúncio](ads/ad-start.md) | Anúncios | [Início do anúncio](/help/reporting/metrics/ad-starts.md) |
| [Anúncio concluído](ads/ad-complete.md) | Anúncios | [Anúncio concluído](/help/reporting/metrics/ad-completes.md) |
| [Ignorar anúncio](ads/ad-skip.md) | Anúncios | — |
| [Pausa do anúncio concluída](ads/ad-break-complete.md) | Anúncios | — |
| [Início do capítulo](chapters/chapter-start.md) | Capítulos | [Início do capítulo](/help/reporting/metrics/chapter-starts.md) |
| [Capítulo concluído](chapters/chapter-complete.md) | Capítulos | [Capítulo concluído](/help/reporting/metrics/chapter-completes.md) |
| [Capítulo ignorado](chapters/chapter-skip.md) | Capítulos | — |
| [Início do estado](player-state/state-start.md) | Estado do player | Varia por estado |
| [Fim do estado](player-state/state-end.md) | Estado do player | Varia por estado |
| [Erro](error.md) | Qualidade | [Fluxos afetados pelo erro](/help/reporting/metrics/error-impacted-streams.md) |

>[!MORELIKETHIS]
>
>* [Esquemas de validação JSON](/help/implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md): verifique a estrutura de carga da solicitação para cada tipo de evento
>* [Ponto de extremidade de solicitação de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md): referência de ponto de extremidade da API Media Collection
>* [Ponto de extremidade de solicitação de sessões](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md): criar uma sessão antes de enviar eventos
>* [Rastreamento do estado do player](/help/use-cases/player-state-tracking/implementation-and-reporting.md): detalhes de implementação do início e do fim do estado
