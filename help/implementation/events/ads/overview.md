---
title: Rastrear anúncios
description: Visão geral da implementação do rastreamento de anúncios com o SDK de mídia.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 513
ht-degree: 3%

---


# Rastrear anúncios

O rastreamento da reprodução do anúncio cobre ad breaks, anúncios iniciados, anúncios concluídos e anúncios ignorados. Use a API do reprodutor de mídia para identificar eventos importantes do reprodutor e preencher as variáveis de anúncio necessárias.

## Eventos do player

| Evento do reprodutor | Ação |
| --- | --- |
| Início de ad break | Criar objeto ad break, chamar AdBreakStart |
| Início do anúncio | Criar objeto de anúncio; chamar AdStart |
| Anúncio concluído | Chamar AdComplete |
| Ignorar anúncio | Chamar AdSkip |
| Ad break concluído | Chamar AdBreakComplete |

## Etapas da implementação

1. Identifique o início do limite do ad break, incluindo o anúncio precedente, e crie um objeto de ad break. Consulte [Nome da interrupção do anúncio](/help/implementation/variables/ads/ad-break-name.md) e [Hora de início da interrupção do anúncio](/help/implementation/variables/ads/ad-break-start-time.md) para obter as definições de campo.
1. Chame [Ad break start](/help/implementation/events/ads/ad-break-start.md) para começar a rastrear o ad break.
1. Identifique o início do anúncio e crie um objeto de anúncio. Consulte [Ad name](/help/implementation/variables/ads/ad-name.md), [Ad ID](/help/implementation/variables/ads/ad-id.md), [Ad length](/help/implementation/variables/ads/ad-length.md), [Ad in pod position](/help/implementation/variables/ads/ad-in-pod-position.md) e [Ad player name](/help/implementation/variables/ads/ad-player-name.md) para obter as definições de campo.
1. Opcionalmente, anexe os metadados de anúncio padrão. Consulte [Anunciante](/help/implementation/variables/ads/advertiser.md), [ID da Campanha](/help/implementation/variables/ads/campaign-id.md), [ID do Creative](/help/implementation/variables/ads/creative-id.md), [URL do Creative](/help/implementation/variables/ads/creative-url.md), [ID de Posicionamento](/help/implementation/variables/ads/placement-id.md) e [ID do Site](/help/implementation/variables/ads/site-id.md) para obter as chaves disponíveis.
1. Chame [Ad start](/help/implementation/events/ads/ad-start.md) para começar a rastrear o anúncio.
1. Quando o anúncio for reproduzido até a conclusão, chame [Anúncio concluído](/help/implementation/events/ads/ad-complete.md).
1. Se o visualizador ignorou o anúncio, chame [Ad skip](/help/implementation/events/ads/ad-skip.md) em vez de Ad complete.
1. Para anúncios adicionais no mesmo ad break, repita as etapas 3 a 7.
1. O ad break está concluído, chame [Ad break concluído](/help/implementation/events/ads/ad-break-complete.md).

>[!IMPORTANT]
>
>**Anúncios precedentes: não chame `trackPlay` antes de `AdBreakStart` e `AdStart`.** O primeiro ping `play` no conteúdo principal incrementa [Início do conteúdo](/help/reporting/metrics/content-starts.md). Se `trackPlay` for chamado antes dos eventos de anúncio precedentes serem acionados e o visualizador sair durante o anúncio, o Início do conteúdo será incrementado mesmo se nenhum conteúdo principal tiver sido reproduzido. Para cenários antes da exibição, atrase `trackPlay` até depois de `AdBreakStart` e `AdStart` terem sido enviados.

>[!NOTE]
>
>O valor do indicador de reprodução relatado durante a reprodução do anúncio representa a posição do visualizador no **conteúdo principal**, não dentro do anúncio. Para um anúncio precedente a um vídeo de 10 minutos, o indicador de reprodução é `0` em todo o anúncio. Para um anúncio intermediário que começa na marca de 5 minutos, o indicador de reprodução permanece em `300` (segundos) durante a duração do anúncio.

## Problemas comuns

### Chamadas :play principais inesperadas entre anúncios

Se você observar chamadas `main:play` ocorrendo entre anúncios consecutivos, há um intervalo de mais de 250 milissegundos entre a chamada AdComplete e a próxima chamada AdStart. Quando essa lacuna ocorre, o Media SDK retorna ao envio dos pings do conteúdo principal, que podem definir a métrica de inícios de conteúdo antecipadamente para cenários de pré-lançamento.

**Causa:** o Media SDK não tem informações de anúncio definidas e o player está em um estado de reprodução, portanto, ele credita a duração da lacuna ao conteúdo principal.

**Solução:** atrasa a chamada AdComplete para cada anúncio (exceto o último) em vez de chamá-lo imediatamente quando o anúncio terminar. Adicione as chamadas em lote da seguinte maneira:

* Em cada **início de anúncio**: se um anúncio anterior existir e ainda não estiver marcado como concluído, chame AdComplete *antes* de AdStart para o novo anúncio.
* Em cada **fim de ativo de anúncio**: não chame AdComplete imediatamente — adie-o.
* Em **ad break concluído**: chame AdComplete para o último anúncio (se ainda não estiver chamado) e, em seguida, chame AdBreakComplete.

Esse padrão garante que o AdComplete e o próximo AdStart sejam acionados simultaneamente, eliminando qualquer lacuna.
