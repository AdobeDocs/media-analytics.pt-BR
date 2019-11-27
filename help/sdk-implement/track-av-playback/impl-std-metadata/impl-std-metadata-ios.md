---
title: Implementar metadados padrão no iOS
description: Descreve a configuração de metadados de vídeo e anúncio padrão a serem enviados com chamadas de rastreamento no iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementar metadados padrão no iOS {#implement-standard-metadata-on-ios}

## Constantes de metadados

| Nome da constante | Descrição   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constante para anexar os metadados padrão no `MediaInfo ADBMediaObject` |

## Implementação

1. Crie um dicionário com os pares de valores dos principais metadados padronizados usando o `ADBStandardMetadataKeys`
   [Chaves de metadados de iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Defina o dicionário de metadados padrão na instância `MediaInfo``ADBMediaObject` usando a constante de Metadados padrão para os metadados.

1. Forneça este objeto `MediaInfo` enquanto invoca a API `trackSessionStart`

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

