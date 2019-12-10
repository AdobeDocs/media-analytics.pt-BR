---
title: Busca de faixa no JavaScript
description: Este tópico descreve como implementar o monitoramento de busca usando o SDK do Media em aplicativos de navegador (JS).
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Busca de faixa no JavaScript {#track-seeking-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de rastreamento de busca

| Nome da constante | Descrição     |
|---|---|
| `SeekStart` | Constante para rastrear o evento Seek Start. |
| `SeekComplete` | Constante para rastrear o evento Seek Complete. |

## Implemente a busca

1. Analise os eventos de busca de reprodução no reprodutor de mídia e, na notificação do evento de início da busca, rastreie a busca com o evento`SeekStart`:

   ```js
   _onSeekStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
   };
   ```

1. Na notificação de conclusão da busca do reprodutor de mídia, rastreie o término da busca com o evento`SeekComplete`:

   ```js
   _onSeekComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
   };
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com busca no conteúdo principal](/help/sdk-implement/tracking-scenarios/vod-seeking.md) para obter mais informações.
