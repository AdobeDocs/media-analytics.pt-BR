---
title: Rastrear buffering no Roku
description: Descreve eventos de rastreamento de buffering no Roku.
uuid: 6666b270-9aa3-42ff-95a8-f12502022d47
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear buffering no Roku {#track-buffering-on-roku}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de rastreamento de buffer

| Nome da constante | Descrição     |
|---|---|
| `BufferStart` | Constante para rastrear o evento Buffer Start |
| `BufferComplete` | Constante para rastrear o evento Buffer Complete |

## Implementar buffering

1. Analise os eventos de buffering de reprodução no reprodutor de mídia e, na notificação do evento de início de buffering, rastreie o buffering usando o evento `BufferStart`.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_START, bufferInfo, bufferContextData)
   ```

1. Na notificação de conclusão de buffer do reprodutor de mídia, rastreie o término do buffer com o evento `BufferComplete`:

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_COMPLETE, bufferInfo, bufferContextData)
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) para obter mais informações.
