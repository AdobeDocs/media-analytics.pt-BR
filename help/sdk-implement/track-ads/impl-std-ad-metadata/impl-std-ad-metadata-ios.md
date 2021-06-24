---
title: Saiba como implementar metadados de anúncio padrão no iOS
description: Como usar metadados de anúncio padrão no rastreamento de anúncios no iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 86%

---

# Implementar Metadados de publicidade padrão no iOS{#implement-standard-ad-metadata-on-ios}

## Constantes de anúncio

| Nome da constante | Descrição   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constante para anexar os metadados de anúncio padrão no `AdInfo ADBMediaObject` |

## Implementar Metadados de publicidade padrão

Para metadados de anúncios padrão, crie um dicionário de pares de valores-chave de metadados de anúncios padrão usando as chaves da sua plataforma:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Chaves de metadados de iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
