---
seo-title: Configurar Roku
title: Configurar Roku
uuid: 904dfda0-4782-41da-b4ab-212e81156633
translation-type: tm+mt
source-git-commit: ab400b673e97f9b47c6088e09b7e7d9e7b1c9ee6

---


# Configurar Roku{#set-up-roku}

## Pré-requisitos

* **Obtain valid configuration parameters for Heartbeats
These parameters can be obtained from an Adobe representative after you set up your media analytics account.**
* **Forneça os seguintes recursos no reprodutor de mídia:**
   * _Uma API para assinar os eventos do reprodutor_ - O SDK do Media exige a chamada de um conjunto de APIs simples quando ocorrerem eventos no reprodutor.
   * _Uma API que fornece informações sobre o reprodutor_ - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

O Adobe Mobile Services apresenta uma nova interface do usuário que reúne recursos de marketing móvel para aplicativos móveis na Adobe Experience Cloud. Inicialmente, o Mobile Service fornece uma integração simples de recursos de análise e segmentação de aplicativos para as soluções do Adobe Analytics e do Adobe Target.

Saiba mais pela [documentação do Adobe Mobile Services.](https://marketing.adobe.com/resources/help/en_US/mobile/)

O SDK do Roku 2.x para soluções da Experience Cloud permite avaliar aplicativos Roku criados com BrightScript, dimensionar e coletar dados de público por meio do gerenciamento de público-alvo e medir o envolvimento com o vídeo pelas pulsações de vídeo.

## Implementação do SDK

1. Adicione a biblioteca [baixada](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) do Roku ao projeto.

   1. The `AdobeMobileLibrary-2.*-Roku.zip` download file consists of the following software components:

      * `adbmobile.brs`: Esse arquivo de biblioteca será incluído na pasta de origem do aplicativo Roku.

      * `ADBMobileConfig.json`: Esse arquivo de configuração do SDK foi personalizado para o aplicativo.
   1. Adicione o arquivo da biblioteca e o arquivo de configuração JSON à origem do projeto.

      O JSON usado para configurar o Adobe Mobile tem uma chave exclusiva para o Media Heartbeats chamada `mediaHeartbeat`. Os parâmetros de configuração do Media Heartbeats pertencem a essa chave.

      >[!TIP]
      >
      >A sample `ADBMobileConfig` JSON file is provided with the package. Entre em contato com seu representante da Adobe para obter as configurações.

      Por exemplo:

      ```
      {
        "version":"1.0", 
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8", 
          "ssl":false, 
          "offlineEnabled":false, 
          "lifecycleTimeout":30, 
          "batchLimit":50, 
          "privacyDefault":"optedin", 
          "poi":[ ]
      },
      "marketingCloud":{
        "org":""
      },
      "target":{ 
        "clientCode":"", 
        "timeout":5
      },
      "audienceManager":{ 
        "server":""
      },
      "acquisition":{ 
        "server":"example.com",
        "appid":"sample-app-id"
      },
      
      "mediaHeartbeat":{ 
         "server":"example.com", 
         "publisher":"sample-publisher", 
         "channel":"sample-channel", 
         "ssl":false,
         "ovp":"sample-ovp", 
         "sdkVersion":"sample-sdk", 
         "playerName":"roku"
         }    
      }
      ```

      | Parâmetro de configuração | Descrição     |
      | --- | --- |
      | `server` | Sequência de caracteres que representa o URL do endpoint de rastreamento no back-end. |
      | `publisher` | Sequência de caracteres que representa o identificador exclusivo do publicador de conteúdo. |
      | `channel` | Sequência de caracteres que representa o nome do canal de distribuição de conteúdo. |
      | `ssl` | Booleano que representa se o SSL deve ser usado para chamadas de rastreamento. |
      | `ovp` | Sequência de caracteres que representa o nome do provedor do reprodutor de vídeo. |
      | `sdkversion` | Sequência de caracteres que representa a versão atual do aplicativo/SDK. |
      | `playerName` | Sequência de caracteres que representa o nome do reprodutor. |

      >[!IMPORTANT]
      >
      >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.


1. Configurar a ID de visitante da Experience Cloud.

   O serviço de ID de visitante da Experience Cloud fornece uma ID de visitante universal em todas as soluções da Experience Cloud. O serviço de ID de visitante é exigido pelo Video Heartbeat e por outras integrações da Experience Cloud.

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```
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

   |  Método   | Descrição |
   | --- | --- |
   | `visitorMarketingCloudID` | Recupera a ID de visitante da Experience Cloud do serviço de ID de visitante.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Com a ID de visitante da Experience Cloud, é possível definir IDs adicionais de clientes que podem ser associadas a cada visitante. A API de visitante aceita várias IDs do cliente para o mesmo visitante e um identificador de tipo de cliente para separar o escopo de diferentes IDs do cliente. This method corresponds to . `setCustomerIDs` For example: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Used to set the Roku ID for Advertising (RIDA) on the SDK. Por exemplo: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>   Get the Roku ID for Advertising (RIDA) using the Roku SDK getRIDA() API.`"<sample_roku_identifier_for_advertising>")`<br/><br/><br/>[](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) |

   <!--
    Roku Api Reference: 
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->
