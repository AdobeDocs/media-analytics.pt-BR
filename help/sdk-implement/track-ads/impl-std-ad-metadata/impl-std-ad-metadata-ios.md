---
description: 'null'
seo-description: 'null'
seo-title: Implementar Metadados de publicidade padrão no iOS
title: Implementar Metadados de publicidade padrão no iOS
uuid: f 15 fb 727-5 a 5 b -46 c 5-bf 12-93 b 376 c 10 fd 1
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implementar Metadados de publicidade padrão no iOS{#implement-standard-ad-metadata-on-ios}

## Constantes do anúncio

| Nome da constante | Descrição  |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## Direcionamento de metadados padrão de anúncio

Para metadados de anúncio padrão, crie um dicionário com os pares de valores dos principais metadados padronizados de anúncio usando as teclas para a sua plataforma:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Chaves de metadados de iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
