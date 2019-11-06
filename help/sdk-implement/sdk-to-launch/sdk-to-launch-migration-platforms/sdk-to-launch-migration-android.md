---
seo-title: Migração do SDK de mídia independente para o Adobe Launch - Android
title: Migração do SDK de mídia independente para o Adobe Launch - Android
seo-description: Instruções e exemplos de código para auxiliar na migração do SDK de mídia para o Launch para Android.
description: Instruções e exemplos de código para auxiliar na migração do SDK de mídia para o Launch para Android.
translation-type: tm+mt
source-git-commit: b479f6623566b6a6989f625b757a97bba5f6aafd

---


# Migração do SDK de mídia independente para o Adobe Launch - Android

## Configuração

### Iniciar Extensão

1. Em Experience Platform Launch, clique na guia [!UICONTROL Extensões] para sua propriedade móvel.
1. Na guia [!UICONTROL Catálogo] , localize a extensão Adobe Media Analytics para áudio e vídeo e clique em [!UICONTROL Instalar].
1. Na página de configurações de extensão, defina os parâmetros de rastreamento.
A extensão de mídia usará os parâmetros configurados para rastreamento.

[Uso de extensões móveis](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

### SDK de mídia independente

No SDK de mídia independente, você configura o rastreamento no aplicativo e o transmite para o SDK ao criar o rastreador.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeat tracker = new MediaHeartbeat(... , config);
```

## Criação do rastreador

### Iniciar Extensão

[Referência da API de mídia - Criar um rastreador de mídia](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Antes de criar o rastreador, você deve registrar a extensão de mídia e as extensões dependentes no núcleo móvel.

```java
// Register the extension once during app launch
try {
    // Media needs Identity and Analytics extension 
    // to function properly
    Identity.registerExtension();
    Analytics.registerExtension();

    // Initialize media extension.
    Media.registerExtension();                
    MobileCore.start(new AdobeCallback () {
        @Override
        public void call(Object o) {
            // Launch mobile property to pick extension settings.
            MobileCore.configureWithAppID("LAUNCH_MOBILE_PROPERTY");
        }
    });
} catch (InvalidInitException ex) {
    ...
}
```

Depois de registrar a extensão de mídia, crie o rastreador usando a seguinte API.
O rastreador escolhe automaticamente a configuração da propriedade de inicialização configurada.

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

### SDK de mídia independente

No SDK de mídia independente, crie manualmente o objeto `MediaHeartbeatConfig` e configure os parâmetros de rastreamento. Implemente a interface delegada expondo`getQoSObject()` e `getCurrentPlaybackTime()functions.`Crie uma `MediaHeartbeat` instância para rastreamento.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeatDelegate delegate = new MediaHeartbeatDelegate() {
    @Override 
    public MediaObject getQoSObject() {
        // When called should return the latest qos values.
        return MediaHeartbeat.createQoSObject(<bitrate>,  
                                              <startupTime>,  
                                              <fps>,  
                                              <droppedFrames>); 
    } 

    @Override 
    public Double getCurrentPlaybackTime() { 
        // When called should return the current player time in seconds.
        return <currentPlaybackTime>; 
    }

    MediaHeartbeat tracker = new MediaHeartbeat(delegate, config);
}
```

## Atualização dos valores de Indicador de reprodução e Qualidade da experiência.

### Iniciar Extensão

A implementação deve atualizar o indicador de reprodução atual chamando o método exposto pelo`updateCurrentPlayhead` rastreador. Para um rastreamento preciso, você deve chamar esse método pelo menos uma vez por segundo.

[Referência da API de mídia - Atualizar player atual](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

A implementação deve atualizar as informações de QoE chamando o `updateQoEObject`método exposto pelo rastreador. Esperamos que esse método seja chamado sempre que houver uma mudança nas métricas de qualidade.

[Referência da API de mídia - Atualizar objeto QoE](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

### SDK de mídia independente

No SDK de mídia independente, você passa um objeto delegado que implementa a interface durante a criação do rastreador`MediaHeartbeartDelegate` .  A implementação deve retornar o QoE e o indicador de reprodução mais recentes sempre que o rastreador chamar os`getQoSObject()` métodos de interface e os métodos de `getCurrentPlaybackTime()` interface.

## Transmissão de metadados padrão de mídia/anúncio

### Iniciar Extensão

* Metadados de mídia padrão:

   ```java
   HashMap<String, Object> mediaObject = 
     Media.createMediaObject("media-name", 
                             "media-id", 
                             60D, 
                             MediaConstants.StreamType.VOD, 
                             Media.MediaType.Video);
   
   HashMap<String, String> mediaMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE, 
                     "Sample Episode");
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW, 
                     "Sample Show");
   
   // Custom metadata keys
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Metadados de publicidade padrão:

   ```java
   HashMap<String, Object> adObject = 
     Media.createAdObject("ad-name", 
                          "ad-id", 
                          1L, 
                          15D);
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER, 
                  "Sample Advertiser");
   adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID, 
                  "Sample Campaign");
   
   // Custom metadata keys
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   _tracker.trackEvent(Media.Event.AdStart, 
                       adObject, 
                       adMetadata);
   ```

### SDK de mídia independente

* Metadados de mídia padrão:

   ```java
   MediaObject mediaInfo = 
     MediaHeartbeat.createMediaObject("media-name", 
                                      "media-id", 
                                      60D, 
                                      MediaHeartbeat.StreamType.VOD, 
                                      MediaHeartbeat.MediaType.Video);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardVideoMetadata = 
     new HashMap<String, String>(); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, 
                             "Sample Episode"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, 
                             "Sample Show"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, 
                             "Sample Season"); 
   mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata, 
                      standardVideoMetadata);
   
   // Custom metadata keys
   HashMap<String, String> mediaMetadata = new HashMap<String, String>();
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Metadados de publicidade padrão:

   ```java
   MediaObject adInfo = 
     MediaHeartbeat.createAdObject("ad-name", 
                                   "ad-id", 
                                   1L, 
                                   15D);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardAdMetadata = 
     new HashMap<String, String>(); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, 
                          "Sample Advertiser"); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, 
                          "Sample Campaign"); 
   adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, 
                   standardAdMetadata); 
   
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   
   tracker.trackEvent(MediaHeartbeat.Event.AdStart, 
                      adObject, 
                      adMetadata);
   ```


