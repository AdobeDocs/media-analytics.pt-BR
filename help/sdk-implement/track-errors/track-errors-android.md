---
seo-title: Rastrear erros no Android
title: Rastrear erros no Android
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Rastrear erros no Android{#track-errors-on-android}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

1. Rastrear erros do player de mídia:

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>O rastreamento de erros do player de mídia não interrompe a sessão de rastreamento de mídia. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

