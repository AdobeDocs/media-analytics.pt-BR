---
seo-title: Configurar Chromecast
title: Configurar Chromecast
uuid: d 664 e 394-02 a 2-4985-bbad-be 1 bcc 44 fb 2 b
translation-type: tm+mt
source-git-commit: ab400b673e97f9b47c6088e09b7e7d9e7b1c9ee6

---


# Configurar Chromecast{#set-up-chromecast}

## Perguntas frequentes

_Devo usar o SDK de JavaScript do Chromecast ou posso usar o SDK do JavaScript padrão?_

A resposta correta é "Chromecast", pelos seguintes motivos:
* As bibliotecas AppMeasurement e VisitorAPI no SDK de JS padrão não são certificadas para funcionar em plataformas OTT. No SDK de JS do Chromecast, a Biblioteca de vídeo do Heartbeat (BVS), o Analytics e a VisitorAPI são todos integrados ao SDK único, unificado e certificado para o Chromecast.
* O SDK do Chromecast é muito mais leve do que o SDK de JS padrão. Isso é muito importante para o hardware de baixo custo usado pelas plataformas OTT.

## Pré-requisitos

* **Obter parâmetros de configuração válidos para o Heartbeats**
Esses parâmetros podem ser obtidos por um representante da Adobe depois que você configurar sua conta de análise de mídia.
* **Forneça os seguintes recursos no reprodutor de mídia:**
   * *Uma API para assinar os eventos do reprodutor* - O SDK do Media exige a chamada de um conjunto de APIs simples quando ocorrerem eventos no reprodutor.
   * *Uma API que fornece informações sobre o reprodutor* - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

O Adobe Mobile Services apresenta uma nova interface do usuário que reúne recursos de marketing móvel para aplicativos móveis na Adobe Experience Cloud. Inicialmente, o Mobile Service fornece uma integração simples de recursos de análise e segmentação de aplicativos para as soluções do Adobe Analytics e do Adobe Target. Saiba mais pela [documentação do Adobe Mobile Services.](https://marketing.adobe.com/resources/help/en_US/mobile/)

O SDK do Chromecast 2.x para soluções da Experience Cloud permite avaliar aplicativos Chromecast criados com JavaScript, dimensionar e coletar dados de público-alvo por meio do gerenciamento de público-alvo e medir o envolvimento com o vídeo pelos heartbeats de vídeo.

## Implementação do SDK

1. Adicione a biblioteca [baixada](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) do Chromecast ao projeto.

   1. O arquivo `AdobeMobileLibrary-Chromecast-[version]` zip consiste nos seguintes componentes de software:

      * `adbmobile-chromecast.min.js`:

         Esse arquivo de biblioteca será incluído na pasta de origem do aplicativo Chromecast.

      * `ADBMobileConfig` config

         Esse arquivo de configuração do SDK foi personalizado para o aplicativo. A sample `ADBMobileConfig` implementation is provided with the SDK (under `samples/`). Obtenha as configurações apropriadas de um representante da Adobe.
   1. Adicione o arquivo de biblioteca ao seu arquivo `index.html` e crie a variável global `ADBMobileConfig` da seguinte maneira (a variável global usada para configurar o Adobe Mobile para Heartbeats tem uma chave exclusiva denominada `mediaHeartbeat`):

      ```js
      <script> 
          var ADBMobileConfig = { 
            "marketingCloud": { 
              "org": "972C898555E9F7BC7F000101@AdobeOrg" 
            }, 
            "target": { 
              "clientCode": "", 
              "timeout": 5 
            }, 
            "audienceManager": { 
              "server": "obumobile5.demdex.net" 
            }, 
            "analytics": { 
              "rsids": "mobile5vhl.sample.player", 
              "server": "obumobile5.sc.omtrdc.net", 
              "ssl": false, 
              "offlineEnabled": false, 
              "charset": "UTF-8", 
              "lifecycleTimeout": 300, 
              "privacyDefault": "optedin", 
              "batchLimit": 0, 
              "timezone": "MDT", 
              "timezoneOffset": -360, 
              "referrerTimeout": 0, 
              "poi": [] 
            }, 
            "mediaHeartbeat": { 
              "server": "obumobile5.hb.omtrdc.net", 
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg", 
              "channel": "test-channel-chromecast", 
              "ssl": false, 
              "ovp": "chromecast-player", 
              "sdkVersion": "chromecast-sdk", 
              "playerName": "Chromecast" 
            } 
          }; 
        </script> 
      <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
      ```

      >[!IMPORTANT]
      >
      >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.

      Parâmetros de configuração do ADBMobile para a chave mediaHeartbeat:
   | Parâmetro de configuração | Descrição     |
   | --- | --- |
   | `server` | Sequência de caracteres que representa o URL do endpoint de rastreamento no back-end. |
   | `publisher` | Sequência de caracteres que representa o identificador exclusivo do publicador de conteúdo. |
   | `channel` | Sequência de caracteres que representa o nome do canal de distribuição de conteúdo. |
   | `ssl` | Booleano que representa se o SSL deve ser usado para chamadas de rastreamento. |
   | `ovp` | Sequência de caracteres que representa o nome do provedor do reprodutor de vídeo. |
   | `sdkversion` | Sequência de caracteres que representa a versão atual do aplicativo/SDK. |
   | `playerName` | Sequência de caracteres que representa o nome do reprodutor. |


1. Configurar a ID de visitante da Experience Cloud.

   O serviço de ID de visitante da Experience Cloud fornece uma ID de visitante universal em todas as soluções da Experience Cloud. O serviço de ID de visitante é exigido pelo Video Heartbeat e por outras integrações da Experience Cloud.

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```js
   "marketingCloud": { 
       "org": YOUR-MCORG-ID" 
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Ensure that you include `@AdobeOrg`.

   Após a configuração ser concluída, uma ID de visitante da Experience Cloud é gerada e incluída em todas as ocorrências. Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Métodos do Serviço de ID de visitante da Experience Cloud.**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   | Método | Descrição |
   | --- | --- |
   | `getMarketingCloudID()` | Recupera a ID de visitante da Experience Cloud do serviço de ID de visitante.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Com a ID de visitante da Experience Cloud, é possível definir IDs adicionais de clientes que podem ser associadas a cada visitante. A API de visitante aceita várias IDs do cliente para o mesmo visitante e um identificador de tipo de cliente para separar o escopo de diferentes IDs do cliente. Este método corresponde a `setCustomerIDs()` na biblioteca do JavaScript.  For example: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |


<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->

