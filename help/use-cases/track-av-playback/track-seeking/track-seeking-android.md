---
title: Saiba como rastrear a busca no Android
description: Saiba como rastrear os eventos de Início da busca e Conclusão da busca usando o SDK de mídia no Android.
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
exl-id: 8a8fcbcf-3232-4565-8c27-4167b6741613
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '130'
ht-degree: 100%

---

# Busca de faixa no Android{#track-seeking-on-android}

As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x.

>[!IMPORTANT]
>
>Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/getting-started/download-sdks.md)

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

Consulte o cenário de rastreamento [Reprodução de VOD com busca no conteúdo principal](/help/use-cases/tracking-scenarios/vod-seeking.md) para obter mais informações.
