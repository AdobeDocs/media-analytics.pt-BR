---
title: Saiba como implementar metadados de anúncio padrão no Roku
description: Como usar metadados de anúncio padrão no rastreamento de anúncio no Roku.
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
exl-id: d2c0a1e0-8d40-4f60-a82d-5860550ac152
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '50'
ht-degree: 100%

---

# Implementar metadados de publicidade padrão no Roku {#implement-standard-ad-metadata-on-roku}

## Implementar Metadados de publicidade padrão

Para metadados de anúncios padrão, crie um dicionário de pares de valores-chave de metadados de anúncios padrão usando as chaves da sua plataforma:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```
