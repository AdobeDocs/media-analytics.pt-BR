---
title: Saiba como implementar metadados padrão no Roku
description: Saiba como configurar metadados de vídeo e anúncios padrão a serem enviados com chamadas de rastreamento no Roku.
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
exl-id: 1552b16a-3c2d-4caa-b571-e6628f0b6866
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '63'
ht-degree: 100%

---

# Implementar metadados padrão no Roku {#implement-standard-metadata-on-roku}

Exemplifique um objeto de metadados padrão, preencha as variáveis desejadas e defina o objeto de metadados no objeto de Heartbeat de mídia.

**Vídeo:**

```
standardMetadata = {}
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show"
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season"
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata
```

**Áudio:**

```
standardMetadata = {}
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist"
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album"
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata
```

Consulte a lista completa de metadados de vídeo aqui: [Parâmetros de áudio e vídeo](/help/implementation/variables/audio-video-parameters.md)
