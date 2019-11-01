---
title: Implementar Metadados de publicidade padrão no Roku
description: Como usar metadados de anúncio padrão no rastreamento de anúncio no Roku.
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementar Metadados de publicidade padrão no Roku{#implement-standard-ad-metadata-on-roku}

## Implementação de metadados de anúncio padrão

Para metadados de anúncio padrão, crie um dicionário de pares de valores principais de metadados de anúncio padrão usando as chaves para sua plataforma:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

