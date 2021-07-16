---
title: Saiba como rastrear o buffering no iOS
description: Saiba como rastrear eventos de buffering no iOS.
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
exl-id: 5f0a3c4b-7c9e-499d-98d0-6fcf316c4d9c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 87%

---

# Rastrear buffering no iOS{#track-buffering-on-ios}

As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x.

>[!IMPORTANT]
>
>Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de rastreamento de buffer


| Nome da constante | Descrição     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Constante para rastrear o evento Buffer Start |
| `ADBMediaHeartbeatEventBufferComplete` | Constante para rastrear o evento Buffer Complete |

## Implementar buffering

1. Analise os eventos de buffering de reprodução no reprodutor de mídia e, na notificação do evento de início de buffering, rastreie o buffering usando o evento`BufferStart`:

   ```
   - (void)onBufferStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Na notificação de conclusão de buffer do reprodutor de mídia, rastreie o término do buffer com o evento`BufferComplete`:

   ```
   - (void)onBufferComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) para obter mais informações.
