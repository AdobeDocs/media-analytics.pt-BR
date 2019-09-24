---
description: 'null'
seo-description: 'null'
seo-title: Implementar Metadados de publicidade padrão no Android
title: Implementar Metadados de publicidade padrão no Android
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Implementar Metadados de publicidade padrão no Android{#implement-standard-ad-metadata-on-android}

## Constantes de anúncio

| Nome da constante | Descrição  |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constante para anexar os Metadados de publicidade padrão ao `MediaObject` do anúncio. |

## Implementação de metadados de anúncio padrão

Para metadados de anúncio padrão, crie um dicionário de pares de valores principais de metadados de anúncio padrão usando as chaves para sua plataforma:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

