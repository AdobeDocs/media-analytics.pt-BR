---
title: Saiba como implementar metadados padrão no iOS
description: Saiba como configurar metadados padrão de vídeo e anúncio para serem enviados com chamadas de rastreamento no iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Gs0IwHZBqv30zfdJ6rdnacIu-1RoDRD9wRaQjK0Q45c
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 100
ht-degree: 89%

---

# Implementar metadados padrão no iOS{#implement-standard-metadata-on-ios}

## Constantes de metadados

| Nome da constante | Descrição   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constante para anexar os metadados padrão no `MediaInfo ADBMediaObject` |

## Implementação

1. Crie um dicionário com os pares de valores dos principais metadados padronizados usando o `ADBStandardMetadataKeys`
   [Chaves de metadados de iOS](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Defina o dicionário de metadados padrão na instância `MediaInfo` `ADBMediaObject` usando a constante de Metadados padrão para os metadados.

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
