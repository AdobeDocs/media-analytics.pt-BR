---
title: Implementação de metadados de anúncio padrão usando o JavaScript 2.x
description: Como usar metadados de anúncio padrão no rastreamento de anúncio em um navegador usando aplicativos JavaScript 2.x.
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 30ed54924c75a9c33e6122b2d7ddbb84c06b8c0c
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 55%

---


# Implementação de metadados de anúncio padrão usando o JavaScript 2.x{#implement-standard-ad-metadata-on-javascript}

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
