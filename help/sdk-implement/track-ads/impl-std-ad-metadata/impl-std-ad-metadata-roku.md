---
description: 'null'
seo-description: 'null'
seo-title: Implementar Metadados de publicidade padrão no Roku
title: Implementar Metadados de publicidade padrão no Roku
uuid: 20 a 437 d 7-18 b 8-4099-ac 81-9 f 3628384236
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Implementar Metadados de publicidade padrão no Roku{#implement-standard-ad-metadata-on-roku}

## Direcionamento de metadados padrão de anúncio

Para metadados de anúncio padrão, crie um dicionário com os pares de valores dos principais metadados padronizados de anúncio usando as teclas para a sua plataforma:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

