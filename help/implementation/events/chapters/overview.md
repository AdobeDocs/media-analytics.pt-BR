---
title: Rastrear capítulos e segmentos
description: Como implementar o rastreamento de capítulo e segmento com o SDK de mídia.
uuid: 3fe32425-5e2a-4886-8fec-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: 'https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg'
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
    internal-label: Implementations
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
    internal-label: Variables
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 39%
---

# Rastrear capítulos e segmentos

O rastreamento de capítulos e segmentos está disponível para capítulos ou segmentos de mídia definidos de forma personalizada. Alguns usos comuns para o rastreamento de capítulos são definir segmentos personalizados com base no conteúdo de mídia (como entradas de beisebol) ou definir segmentos de conteúdo entre ad breaks. O rastreamento de capítulos **não** é necessário para implementações de heartbeat de mídia principais.

O rastreamento do capítulo inclui inícios de capítulo, conclusões de capítulo e capítulos ignorados. Use a API do reprodutor de mídia com lógica de segmentação personalizada para identificar eventos do capítulo e preencher as variáveis do capítulo.

## Eventos do player

| Evento do reprodutor | Ação |
| --- | --- |
| Início do capítulo | Criar objeto de capítulo, chamar ChapterStart |
| Capítulo concluído | Chamar ChapterComplete |
| Capítulo ignorado | Chamar ChapterSkip |

## Etapas da implementação

1. Identifique quando ocorre o evento de início do capítulo e crie o objeto de capítulo. Consulte [Nome do capítulo](/help/implementation/variables/chapters/chapter-name.md), [Posição do capítulo](/help/implementation/variables/chapters/chapter-position.md), [Comprimento do capítulo](/help/implementation/variables/chapters/chapter-length.md) e [Deslocamento do capítulo](/help/implementation/variables/chapters/chapter-offset.md) para obter as definições de campo.
1. Opcionalmente, crie variáveis de dados de contexto para metadados de capítulo personalizados.
1. Chame [Início do capítulo](/help/implementation/events/chapters/chapter-start.md) para começar a rastrear o capítulo.
1. Quando a reprodução atingir o limite final do capítulo, chame [Chapter complete](/help/implementation/events/chapters/chapter-complete.md).
1. Se o usuário ignorar o capítulo antes da conclusão, chame [Chapter skip](/help/implementation/events/chapters/chapter-skip.md).
1. Para capítulos adicionais, repita as etapas de 1 a 5.
