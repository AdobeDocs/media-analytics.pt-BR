---
title: Sobre estados padrão e personalizados
description: Saiba mais sobre o recurso de rastreamento do estado do player, incluindo requisitos e diretrizes para implementar e informar estados padrão e personalizados do player.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/QdUkyWt6cTcdmQXpj6Qe6-s3aYkGfro-G7DYegOVKvA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 287
ht-degree: 96%

---

# Sobre estados padrão e personalizados

Cinco estados padrão do player estão disponíveis e você pode adicionar seus próprios estados personalizados.

| Nome do estado padrão | Constante do SDK de mídia | Nome da API da coleção de mídia |
|-----------------------|------------------------------------------|-----------------------------|
| Tela cheia | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Legendas ocultas | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Mudo | `ADB.Media.PlayerState.Mute` | `mute` |
| Picture in Picture | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| Em foco | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Os dados são calculados da mesma forma para estados padrão e personalizados, mas os dados são armazenados de forma diferente para relatórios do Analytics.

**Para estados padrão** — Ao habilitar o rastreamento do estado do player pelo console de Gerenciamento de mídia nos relatórios do Analytics (lado administrativo), 15 variáveis de solução estão disponíveis para exportações de relatórios e dados.

**Para estados personalizados** — Você pode criar suas próprias regras de processamento para armazenar os valores calculados em eventos personalizados e, em seguida, usar essas regras para exportações de relatórios e dados.

## Diretrizes

* Uma sessão de vídeo é limitada a 10 estados do player.
* Qualquer combinação de estados é permitida.
* Se vários estados do player passarem, apenas os primeiros 10 serão retidos e encaminhados para o componente de processamento do VA.
* O máximo de 10 estados é aplicado a todos os estados, independentemente de estarem fechados ou não.
* Um estado pode ser iniciado e finalizado várias vezes e é contado como um único estado. Por exemplo, `closedCapationing` pode ser iniciado e parado cinco vezes, mas contará como um único estado.
* Todos os estados que excederem o máximo de 10 estados permitidos são descartados.

## Estados personalizados

Com a capacidade de criar estados personalizados, você pode capturar ações personalizadas e atualizar metadados personalizados durante uma sessão de reprodução.

Para obter informações sobre como criar estados personalizados, consulte o [Guia de referência de API de mídia: `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)
