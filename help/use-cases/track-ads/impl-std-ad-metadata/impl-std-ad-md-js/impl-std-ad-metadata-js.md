---
title: Saiba como implementar metadados de anúncio padrão usando o JavaScript 2.x
description: Como usar metadados de anúncio padrão no rastreamento de anúncios em um navegador que utiliza aplicativos JavaScript 2.x.
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
exl-id: b331db87-ab4e-44fa-a97c-9691974cacd4
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 94%

---

# Implementar metadados de anúncio padrão usando o JavaScript 2.x{#implement-standard-ad-metadata-on-javascript}

## Constantes de anúncio

| Nome da constante | Descrição   |
|---|---|
| `StandardAdMetadata` | Constante para anexar os Metadados de publicidade padrão ao objeto do anúncio |

## Implementar Metadados de publicidade padrão

Para metadados de anúncios padrão, crie um dicionário de pares de valores-chave de metadados de anúncios padrão usando as chaves da sua plataforma:

```js
var adObject =  
MediaHeartbeat.createAdObject(<AD_NAME>,  
                              <AD_ID>,  
                              <POSITION>,  
                              <LENGTH>);

// Set standard Ad Metadata
var standardAdMetadata = {};
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
```
