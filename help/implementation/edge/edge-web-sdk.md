---
title: Enviar dados da Web para o Edge com o Adobe Experience Platform Web SDK
description: Saiba como enviar dados de mídia de transmissão do Adobe para o Experience Platform Edge com o Adobe Experience Platform Web SDK.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Enviar dados da Web para o Edge com o Adobe Experience Platform Web SDK

A partir da versão 2.20.0, o componente `streamingMedia` da [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) do Adobe Experience Platform permite que você colete dados relacionados às sessões de mídia no seu site. Os dados coletados podem incluir informações sobre reprodução de mídia, pausas, conclusões e outros eventos relacionados.

Depois que os dados forem coletados, você poderá enviá-los para a Adobe Experience Platform e/ou Adobe Analytics para gerar relatórios. Esse recurso fornece uma solução abrangente para rastrear e entender o comportamento de consumo de mídia no site.

Para clientes que estão usando o Media JS SDK, o Web SDK fornece um caminho de migração do Media JS SDK para o Web SDK, ao mesmo tempo em que inclui suporte para funcionalidades existentes do Media JS, como manipular eventos de mídia.

## Pré-requisitos {#prerequisites}

Para usar o componente `streamingMedia` do Web SDK, você deve atender aos seguintes pré-requisitos:

* Antes de enviar dados de streaming de mídia para a Edge, primeiro conclua as etapas em [Instalar a Coleção de Streaming de Mídia com o Experience Platform Edge](/help/implementation/edge/implementation-edge.md).
* Verifique se você tem acesso ao Adobe Experience Platform e/ou Adobe Analytics.
* Você deve usar o Web SDK versão 2.20.0 ou posterior. Consulte a [visão geral da instalação do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) para saber como instalar a versão mais recente.
* Habilite a opção **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** para a sequência de dados que você está usando.
* Certifique-se de que o esquema usado pelo fluxo de dados inclua os campos de esquema Coleção de mídia.
* Configure o recurso Mídia de Streaming na configuração do Web SDK, conforme mostrado nesta página, por meio da [extensão de tag](#tag-extension) ou da [biblioteca JavaScript](#library).

Siga as etapas descritas nesta página para migrar sua implementação de coleção de mídia de transmissão do Media JS para o Web SDK.

### Etapa 1: instalar o Experience Platform Web SDK

Consulte a [documentação dedicada](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) para saber como instalar o Web SDK nas suas propriedades da Web.

### Etapa 2: configurar o componente `streamingMedia` do Web SDK.

**Exemplo**

O trecho abaixo mostra como configurar a coleção de mídia no Media JS.

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

Em vez disso, você deve configurar o componente `streamingMedia` no Web SDK, como exemplificado abaixo.

```js
alloy("configure", {
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Consulte a [documentação](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) do componente `streamingMedia` do Web SDK para obter detalhes completos sobre como configurá-lo.

### Etapa 3: obtenha a instância do rastreador de mídia ao migrar do Media JS SDK

Para clientes que estão usando o Media JS SDK, o Web SDK fornece um caminho de migração do Media JS SDK para o Web SDK, ao mesmo tempo em que inclui suporte para funcionalidades existentes do Media JS, como manipular eventos de mídia.

[!DNL Web SDK] inclui um comando para recuperar um Media Analytics Tracker. Você pode usar este comando para criar uma instância de objeto e, em seguida, usar as mesmas APIs que as fornecidas pela [biblioteca Media JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), rastrear eventos de mídia.

Consulte a documentação de [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) para obter detalhes completos sobre os métodos compatíveis.

O trecho abaixo mostra como você recuperaria a instância do rastreador de mídia no Media JS.

```javascript
var tracker = ADB.Media.getInstance();
```

Em vez disso, use o comando `getMediaAnalyticsTracker` no Web SDK para obter o mesmo resultado, conforme mostrado abaixo.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Todos os métodos auxiliares estarão disponíveis no objeto `Media`. Os métodos do rastreador estão disponíveis na instância do rastreador, conforme mostrado abaixo.

```js
const mediaInfo = Media.createMediaObject(
  "video name",
  "player video",
  60,
  Media.StreamType.VOD,
  Media.MediaType.Video
);

const contextData = {
  isUserLoggedIn: "false",
  tvStation: "Sample TV station",
  programmer: "Sample programmer",
  assetID: "/uri-reference"
};

// Set standard Video Metadata
contextData[Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[Media.VideoMetadataKeys.Show] = "Sample Show";

trackerInstance.trackSessionStart(mediaInfo, contextData);
```
