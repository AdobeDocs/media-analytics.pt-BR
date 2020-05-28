---
title: Sobre estados padrão e personalizados
description: Este tópico descreve o recurso de rastreamento do estado do player, incluindo requisitos e diretrizes para implementar e relatórios de estados padrão e personalizados do player.
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---


# Sobre estados padrão e personalizados

Cinco estados padrão de player estão disponíveis e você pode adicionar seus próprios estados personalizados.

| Nome do Estado Padrão | Constante do SDK de mídia | Nome da API da coleção de mídia |
|-----------------------|------------------------------------------|-----------------------------|
| Tela cheia | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Legenda fechada | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Silenciar | `ADB.Media.PlayerState.Mute` | `mute` |
| Imagem em imagem | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| Em foco | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Os dados são calculados da mesma forma para estados padrão e personalizados, mas os dados são armazenados de forma diferente para o relatórios do Analytics.

**Para estados** padrão — quando você ativa o rastreamento de estado do player a partir do console de Gerenciamento de mídia no relatórios do Analytics (lado administrativo), 15 variáveis de solução estão disponíveis para exportações de relatórios e dados.

**Para estados** personalizados — Você pode criar suas próprias regras de processamento para armazenar os valores calculados em eventos personalizados e, em seguida, usar essas regras para exportações de relatórios e dados.

## Diretrizes

* Uma sessão de vídeo é limitada a 10 estados de player.
* Qualquer combinação de estados é permitida.
* Se vários estados de player passarem, apenas os primeiros 10 serão retidos e encaminhados para downstream para o componente de processamento VA.
* O máximo de 10 estados é aplicado a todos os estados, independentemente de estarem fechados ou não.
* Um estado pode ser start e finalizado várias vezes e é contado como um único estado. Por exemplo, `closedCapationing` pode ser iniciado e parado cinco vezes, mas contará como um único estado.
* Todos os estados que excederem o máximo de 10 estados permitidos são descartados.

## Estados personalizados

Com a capacidade de criar estados personalizados, você pode capturar ações personalizadas e atualizar metadados personalizados durante uma sessão de reprodução.

Para obter informações sobre como criar estados personalizados, consulte o guia de Referência da API de [mídia: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
