---
description: 'null'
seo-description: 'null'
seo-title: Implementar Metadados de publicidade padrão no iOS
title: Implementar Metadados de publicidade padrão no iOS
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implementar Metadados de publicidade padrão no iOS{#implement-standard-ad-metadata-on-ios}

## Constantes de anúncio

| Nome da constante | Descrição  |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## Implemement standard ad metadata

Para metadados de anúncio padrão, crie um dicionário de pares de valores principais de metadados de anúncio padrão usando as chaves para sua plataforma:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Chaves de metadados de iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
