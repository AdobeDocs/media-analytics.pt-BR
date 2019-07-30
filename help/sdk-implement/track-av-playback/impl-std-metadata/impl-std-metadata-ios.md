---
description: 'null'
seo-description: 'null'
seo-title: Implementar metadados padrão no iOS
title: Implementar metadados padrão no iOS
uuid: 75 a 80 f 08-4 a 95-49 d 4-a 27 a -8 ce 531 d 64 d 31
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implementar metadados padrão no iOS{#implement-standard-metadata-on-ios}

## Constantes de metadados

| Nome da constante | Descrição  |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constante para anexar os metadados padrão no `MediaInfo ADBMediaObject` |

## Implementação

1. Create a dictionary of standard metadata key value pairs using the `ADBStandardMetadataKeys`
   [Teclas de metadados do IOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Defina o dicionário de metadados padrão na instância `MediaInfo``ADBMediaObject`   usando a constante de Metadados padrão para os metadados.

1. Provide this `MediaInfo` object while invoking the `trackSessionStart` API.

### Exemplo de implementação

Exemplifique um objeto de metadados padrão, preencha as variáveis desejadas e defina o objeto de metadados no objeto de Heartbeat de mídia. Por exemplo:

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

