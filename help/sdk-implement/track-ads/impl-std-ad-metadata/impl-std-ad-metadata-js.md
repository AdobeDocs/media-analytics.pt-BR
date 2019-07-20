---
description: 'null'
seo-description: 'null'
seo-title: Implementar Metadados de publicidade padrão no JavaScript
title: Implementar Metadados de publicidade padrão no JavaScript
uuid: 4 ea 10 c 5 a-ae 2 b -45 d 0-aad 3-9 f 10028 ee 7 c 3
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Implementar Metadados de publicidade padrão no JavaScript{#implement-standard-ad-metadata-on-javascript}

## Constantes do anúncio

| Nome da constante | Descrição  |
|---|---|
| `StandardAdMetadata` | Constante para anexar os Metadados de publicidade padrão ao objeto do anúncio |

## Direcionamento de metadados padrão de anúncio

Para metadados de anúncio padrão, crie um dicionário com os pares de valores dos principais metadados padronizados de anúncio usando as teclas para a sua plataforma:

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

