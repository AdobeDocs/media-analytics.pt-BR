---
title: Implementar Metadados de publicidade padrão no Android
description: Como usar metadados de anúncio padrão no rastreamento de anúncios no Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementar Metadados de publicidade padrão no Android {#implement-standard-ad-metadata-on-android}

## Constantes de anúncio

| Nome da constante | Descrição   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constante para anexar os Metadados de publicidade padrão ao `MediaObject` do anúncio. |

## Implementar Metadados de publicidade padrão

Para metadados de anúncios padrão, crie um dicionário de pares de valores-chave de metadados de anúncios padrão usando as chaves da sua plataforma:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

