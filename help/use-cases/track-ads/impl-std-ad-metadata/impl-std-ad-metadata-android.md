---
title: Saiba como implementar metadados de anúncio padrão no Android
description: Como usar metadados de anúncio padrão no rastreamento de anúncios no Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 100%

---

# Implementar metadados de publicidade padrão no Android {#implement-standard-ad-metadata-on-android}

## Constantes de anúncio

| Nome da constante | Descrição   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constante para anexar os Metadados de publicidade padrão ao `MediaObject` do anúncio. |

## Implementar metadados de publicidade padrão

Para metadados de anúncios padrão, crie um dicionário de pares de valores-chave de metadados de anúncios padrão usando as chaves da sua plataforma:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```
