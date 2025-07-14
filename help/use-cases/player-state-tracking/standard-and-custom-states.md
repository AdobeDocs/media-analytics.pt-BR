---
title: Sobre estados padrão e personalizados
description: Saiba mais sobre o recurso de rastreamento do estado do player, incluindo requisitos e diretrizes para implementar e informar estados padrão e personalizados do player.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 99%

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

**Para estados padrão** — Ao ativar o rastreamento do estado do player pelo console de Gerenciamento de mídia nos relatórios do Analytics (lado administrativo), 15 variáveis de solução estão disponíveis para exportações de relatórios e dados.

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
