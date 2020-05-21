---
title: Sobre estados padrão e personalizados
description: Este tópico descreve o recurso de rastreamento do estado do player, incluindo requisitos e diretrizes para implementar e relatórios de estados padrão e personalizados do player.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '251'
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

* Uma sessão de vídeo é limitada a 10 estados de player personalizados.
* Se vários estados de player passarem, apenas os primeiros 10 serão retidos e encaminhados para o componente de processamento VA(?video analytics).
* O máximo de 10 estados é aplicado a todos os estados, independentemente de estarem fechados ou não.
* O mesmo estado pode ser iniciado e encerrado a qualquer número de vezes e é contado como um único estado.
* Todo estado que está excedendo o máximo de costumes permitido? estados (10) são descartados.

## Estados personalizados

Com a capacidade de criar estados personalizados, você pode capturar ações personalizadas e atualizar metadados personalizados durante uma sessão de reprodução.

PRECISAM de mais informações sobre estados personalizados
