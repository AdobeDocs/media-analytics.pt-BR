---
title: Busca de rastreamento usando o JavaScript 3.x
description: Este tópico descreve como implementar o monitoramento de busca usando o SDK do Media em aplicativos de navegador (JS).
translation-type: tm+mt
source-git-commit: 5f274452b9ff5770908f7e2e450935be572a22ea
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 76%

---


# Busca de rastreamento usando o JavaScript 3.x{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de rastreamento de busca

| Nome da constante | Descrição     |
|---|---|
| `SeekStart` | Constante para rastrear o evento Seek Start. |
| `SeekComplete` | Constante para rastrear o evento Seek Complete. |

## Implemente a busca

1. Analise os eventos de busca de reprodução no reprodutor de mídia e, na notificação do evento de início da busca, rastreie a busca com o evento`SeekStart`:

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. Na notificação de conclusão da busca do reprodutor de mídia, rastreie o término da busca com o evento`SeekComplete`:

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com busca no conteúdo principal](/help/sdk-implement/tracking-scenarios/vod-seeking.md) para obter mais informações.
