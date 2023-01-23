---
title: Saiba como rastrear o buffering no Android
description: Saiba como rastrear eventos de buffering no Android.
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
exl-id: fcea2ef8-53c5-41fb-8b70-06599c2d9cbf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '117'
ht-degree: 100%

---

# Rastrear buffering no Android{#track-buffering-on-android}

As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x.

>[!IMPORTANT]
>Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/getting-started/download-sdks.md)

## Constantes de rastreamento de buffer

| Nome da constante | Descrição     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | Constante para rastrear o evento Buffer Start |
| `MediaHeartbeat.Event.BufferComplete` | Constante para rastrear o evento Buffer Complete |

## Implementar buffering

1. Analise os eventos de buffering de reprodução no reprodutor de mídia e, na notificação do evento de início de buffering, rastreie o buffering usando o evento`BufferStart`:

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null);
   }
   ```

1. Na notificação de conclusão de buffer do reprodutor de mídia, rastreie o término do buffer com o evento`BufferComplete`:

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null);
   }
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com buffering](/help/use-cases/tracking-scenarios/vod-buffering.md) para obter mais informações.
