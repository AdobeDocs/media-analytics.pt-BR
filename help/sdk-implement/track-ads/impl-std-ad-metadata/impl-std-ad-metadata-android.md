---
description: 'null'
seo-description: 'null'
seo-title: Implementar Metadados de publicidade padrão no Android
title: Implementar Metadados de publicidade padrão no Android
uuid: 19 b 98 bc 1-c 659-4182-a 4 ff-b 3340 fe 2453 c
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Implementar Metadados de publicidade padrão no Android{#implement-standard-ad-metadata-on-android}

## Constantes do anúncio

| Nome da constante | Descrição  |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constante para anexar os Metadados de publicidade padrão ao `MediaObject` do anúncio. |

## Direcionamento de metadados padrão de anúncio

Para metadados de anúncio padrão, crie um dicionário com os pares de valores dos principais metadados padronizados de anúncio usando as teclas para a sua plataforma:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

