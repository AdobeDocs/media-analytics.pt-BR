---
title: Rastrear busca no Android
description: Este tópico descreve como implementar o rastreamento de busca usando o SDK do Media no Android.
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear busca no Android {#track-seeking-on-android}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de rastreamento de busca

| Nome da constante | Descrição     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Constante para rastrear o evento Seek Start. |
| `MediaHeartbeat.Event.SeekComplete` | Constante para rastrear o evento Seek Complete. |

## Implemente a busca

1. Analise os eventos de busca de reprodução no reprodutor de mídia e, na notificação do evento de início da busca, rastreie a busca com o evento`SeekStart`:

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   }
   ```

1. Na notificação de conclusão da busca do reprodutor de mídia, rastreie o término da busca com o evento`SeekComplete`:

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   }
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com busca no conteúdo principal](/help/sdk-implement/tracking-scenarios/vod-seeking.md) para obter mais informações.
