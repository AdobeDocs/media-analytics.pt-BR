---
title: Busca de faixa no Roku
description: Este tópico descreve a implementação do rastreamento de busca usando o SDK do Media no Roku.
uuid: 0572252b-397f-4aa2-b4b5-c5346b75244a
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Busca de faixa no Roku {#track-seeking-on-roku}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de rastreamento de busca

| Nome da constante | Descrição     |
|---|---|
| `SeekStart` | Constante para rastrear o evento Seek Start. |
| `SeekComplete` | Constante para rastrear o evento Seek Complete. |

## Implemente a busca

1. Analise os eventos de busca de reprodução no reprodutor de mídia e, na notificação do evento de início da busca, rastreie a busca com o evento `SeekStart`:

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_START, seekInfo, seekContextData)
   ```

1. Na notificação de conclusão da busca do reprodutor de mídia, rastreie o término da busca com o evento `SeekComplete`.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_COMPLETE, seekInfo, seekContextData)
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com busca no conteúdo principal](/help/sdk-implement/tracking-scenarios/vod-seeking.md) para obter mais informações.
