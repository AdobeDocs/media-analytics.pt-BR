---
description: 'null'
seo-description: 'null'
seo-title: Implementar Metadados de publicidade padrão no Roku
title: Implementar Metadados de publicidade padrão no Roku
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

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

