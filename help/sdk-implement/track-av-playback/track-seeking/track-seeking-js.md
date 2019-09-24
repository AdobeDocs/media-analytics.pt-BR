---
seo-title: Busca de faixa no JavaScript
title: Busca de faixa no JavaScript
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Busca de faixa no JavaScript{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de rastreamento de busca

| Nome da constante | Descrição     |
|---|---|
| `SeekStart` | Constante para rastrear o evento Seek Start. |
| `SeekComplete` | Constante para rastrear o evento Seek Complete. |

## Implemente a busca

1. Analise os eventos de busca de reprodução no reprodutor de mídia e, na notificação do evento de início da busca, rastreie a busca com o evento `SeekStart`:

   ```js
   _onSeekStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
   };
   ```

1. Na notificação de conclusão da busca do reprodutor de mídia, rastreie o término da busca com o evento `SeekComplete`:

   ```js
   _onSeekComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
   };
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com busca no conteúdo principal](/help/sdk-implement/tracking-scenarios/vod-seeking.md) para obter mais informações.
