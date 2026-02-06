---
title: Saiba como rastrear o buffering usando o JavaScript 3.x
description: Saiba como rastrear eventos de buffering em aplicativos de navegador (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 100%

---

# Rastrear buffering usando o JavaScript 3.x{#track-buffering-on-javascript}

As instruções a seguir fornecem orientação para a implementação em todos os SDKs 3.x.

>[!IMPORTANT]
>
>Se estiver implementando uma versão anterior do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/getting-started/download-sdks.md)

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

Consulte o cenário de rastreamento [Reprodução de VOD com buffering](/help/use-cases/tracking-scenarios/vod-buffering.md) para obter mais informações.
