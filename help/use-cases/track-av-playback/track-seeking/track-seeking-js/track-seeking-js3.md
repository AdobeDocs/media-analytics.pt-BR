---
title: Saiba como rastrear a busca usando o JavaScript 3.x
description: Saiba como rastrear os eventos de Início da busca e Conclusão da busca usando o SDK de mídia em aplicativos de navegador (JS 3.x).
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Rastrear busca usando o JavaScript 3.x{#track-seeking-on-javascript}

As instruções a seguir fornecem orientação para a implementação em todos os SDKs 3.x.

>[!IMPORTANT]
>
>Se estiver implementando uma versão anterior do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/getting-started/download-sdks.md)

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

Consulte o cenário de rastreamento [Reprodução de VOD com busca no conteúdo principal](/help/use-cases/tracking-scenarios/vod-seeking.md) para obter mais informações.
