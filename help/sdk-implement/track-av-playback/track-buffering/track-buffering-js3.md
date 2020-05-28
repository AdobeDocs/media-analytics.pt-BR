---
title: Rastrear buffering usando o JavaScript 3.x
description: Descreve eventos de rastreamento de buffering em aplicativos de navegador (JS).
translation-type: tm+mt
source-git-commit: 8235fee973623c168dbf83f43aa85f13b4e06cff
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 74%

---


# Rastrear buffering usando o JavaScript 3.x{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de rastreamento de buffer

| Nome da constante | Descrição     |
|---|---|
| `BufferStart` | Constante para rastrear o evento Buffer Start |
| `BufferComplete` | Constante para rastrear o evento Buffer Complete |

## Implementar buffering

1. Analise os eventos de buffering de reprodução no reprodutor de mídia e, na notificação do evento de início de buffering, rastreie o buffering usando o evento `BufferStart`.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. Na notificação de conclusão de buffer do reprodutor de mídia, rastreie o término do buffer com o evento`BufferComplete`:

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) para obter mais informações.
