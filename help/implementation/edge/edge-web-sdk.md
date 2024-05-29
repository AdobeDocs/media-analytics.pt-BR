---
title: Enviar dados da Web para o Edge com o SDK da Web da Adobe Experience Platform
description: Saiba como enviar dados de mídia de transmissão do Adobe para o Experience Platform Edge com o SDK da Web da Adobe Experience Platform.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ad40260d29bd5b739184cb551f084565d05e65a7
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Enviar dados da Web para o Edge com o SDK da Web da Adobe Experience Platform

A partir da versão 2.20.0, a variável `streamingMedia` componente do Adobe Experience Platform [SDK da Web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) O permite que você colete dados relacionados a sessões de mídia no seu site. Os dados coletados podem incluir informações sobre reprodução de mídia, pausas, conclusões e outros eventos relacionados.

Depois que os dados forem coletados, você poderá enviá-los para a Adobe Experience Platform e/ou Adobe Analytics para gerar relatórios. Esse recurso fornece uma solução abrangente para rastrear e entender o comportamento de consumo de mídia no site.

Para clientes que estão usando o SDK do Media JS, o SDK da Web fornece um caminho de migração do SDK do Media JS para o SDK da Web, ao mesmo tempo em que inclui suporte para funcionalidades existentes do Media JS, como manipular eventos de mídia.

## Pré-requisitos  {#prerequisites}

Para usar o `streamingMedia` do SDK da Web, você deve atender aos seguintes pré-requisitos:

* Antes de enviar dados do Media Analytics para o Edge, primeiro conclua as etapas em [Instale o Media Analytics com Experience Platform Edge](/help/implementation/edge/implementation-edge.md).
* Verifique se você tem acesso ao Adobe Experience Platform e/ou Adobe Analytics.
* Você deve usar o SDK da Web versão 2.20.0 ou posterior. Consulte a [Visão geral de instalação do SDK da Web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) para saber como instalar a versão mais recente.
* Ativar o **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** opção para a sequência de dados que você está usando.
* Certifique-se de que o esquema usado pelo fluxo de dados inclua os campos de esquema Coleção de mídia.
* Configure o recurso Mídia de transmissão na configuração do SDK da Web, conforme mostrado nesta página, por meio da [extensão de tag](#tag-extension) ou por meio da [Biblioteca JavaScript](#library).

Siga as etapas descritas nesta página para migrar sua implementação do Analytics para mídia de streaming do Media JS para o SDK da Web.

### Etapa 1: instalar o SDK da Web do Experience Platform

Consulte a [documentação dedicada](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) para saber como instalar o SDK da Web nas propriedades da Web.

### Etapa 2: configurar o SDK da Web `streamingMedia` componente.

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

Em vez disso, você deve configurar o `streamingMedia` no SDK da Web, como exemplificado abaixo.

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

Consulte o SDK da Web `streamingMedia` componente [documentação](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) para obter detalhes completos sobre como configurá-lo.

### Etapa 3: obtenha a instância do rastreador de mídia ao migrar do SDK do Media JS

Para clientes que estão usando o SDK do Media JS, o SDK da Web fornece um caminho de migração do SDK do Media JS para o SDK da Web, ao mesmo tempo em que inclui suporte para funcionalidades existentes do Media JS, como manipular eventos de mídia.

[!DNL Web SDK] O inclui um comando para recuperar um Media Analytics Tracker. Você pode usar esse comando para criar uma instância de objeto e, em seguida, usar as mesmas APIs que as fornecidas pelo [Biblioteca JS de mídia](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), rastrear eventos de mídia.

Consulte a [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) para obter detalhes completos sobre os métodos compatíveis.

O trecho abaixo mostra como você recuperaria a instância do rastreador de mídia no Media JS.

```javascript
var tracker = ADB.Media.getInstance();
```

Use o botão `getMediaAnalyticsTracker` no SDK da Web para obter o mesmo resultado, como mostrado abaixo.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Todos os métodos auxiliares estarão disponíveis no `Media` objeto. Os métodos do rastreador estão disponíveis na instância do rastreador, conforme mostrado abaixo.

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
