---
title: Configurar Roku
description: Configuração do aplicativo SDK do Media para implementação no Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Configurar Roku {#set-up-roku}

## Pré-requisitos

* **Obter parâmetros de configuração válidos para Heartbeats** Esses parâmetros podem ser obtidos de um representante da Adobe após a configuração da sua conta do Media Analytics.
* **Forneça os seguintes recursos no player de mídia:**
   * _Uma API para assinar eventos do player_ - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * _Uma API que fornece informações sobre o player_ - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

O Adobe Mobile Services fornece uma nova interface do usuário que reúne recursos de marketing móvel para aplicativos móveis de toda a Adobe Experience Cloud. Inicialmente, o Mobile Service fornece integração perfeita entre os recursos de análise e segmentação de aplicativos para as soluções do Adobe Analytics e do Adobe Target.

Saiba mais pela [documentação do Adobe Mobile Services.](https://docs.adobe.com/content/help/pt-BR/mobile-services/using/home.html)

O SDK do Roku 2.x para soluções da Experience Cloud permite avaliar aplicativos Roku criados com BrightScript, dimensionar e coletar dados de público por meio do gerenciamento de público-alvo e medir o envolvimento com o vídeo pelas pulsações de vídeo.

## Implementação do SDK

1. Adicione a biblioteca [baixada](/help/sdk-implement/download-sdks.md#download-2x-sdks) do Roku ao projeto.

   1. O arquivo de download `AdobeMobileLibrary-2.*-Roku.zip` consiste nos seguintes componentes de software:

      * `adbmobile.brs`: Esse arquivo de biblioteca será incluído na pasta de origem do aplicativo Roku.

      * `ADBMobileConfig.json`: Esse arquivo de configuração do SDK foi personalizado para o aplicativo.
   1. Adicione o arquivo da biblioteca e o arquivo de configuração JSON à origem do projeto.

      O JSON usado para configurar o Adobe Mobile tem uma chave exclusiva para o Media Heartbeats chamada `mediaHeartbeat`. Os parâmetros de configuração do Media Heartbeats pertencem a essa chave.

      >[!TIP]
      >
      >Um exemplo de arquivo JSON `ADBMobileConfig` é fornecido com o pacote. Entre em contato com representantes da Adobe para obter as configurações.

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
      >Se `mediaHeartbeat` for configurado incorretamente, o módulo de mídia (VHL) entrará em um estado de erro e deixará de enviar chamadas de rastreamento.


1. Configurar a ID de visitante da Experience Cloud.

   O serviço de ID de visitante da Experience Cloud fornece uma ID de visitante universal nas soluções da Experience Cloud. O serviço de ID de visitante é exigido pela pulsação de vídeo e outras integrações da Experience Cloud.

   Verifique se a sua configuração `ADBMobileConfig` contém a ID da organização da `marketingCloud`.

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   As IDs de organização da Experience Cloud identificam de forma exclusiva cada empresa de clientes na Adobe Experience Cloud e são semelhantes ao seguinte valor: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Certifique-se de incluir `@AdobeOrg`.

   Após a configuração ser concluída, uma ID de visitante da Experience Cloud é gerada e incluída em todas as ocorrências. Outras IDs de visitante, como `custom` e `automatically-generated`, continuam a ser enviadas com cada ocorrência.

   **Métodos do Serviço de ID de visitante da Experience Cloud.**

   >[!TIP]
   >
   >Os métodos de ID de visitante da Experience Cloud apresentam o prefixo `visitor`.

   |  Método   | Descrição |
   | --- | --- |
   | `visitorMarketingCloudID` | Recupera a ID de visitante da Experience Cloud do serviço de ID de visitante.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Com a ID de visitante da Experience Cloud, é possível definir outras IDs do cliente que podem ser associadas a cada visitante. A API de visitante aceita várias IDs de cliente para o mesmo visitante e um identificador de tipo de cliente para separar o escopo das diferentes IDs de clientes. Este método corresponde a `setCustomerIDs`. Por exemplo: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Usado para definir a ID do Roku para publicidade (RIDA) no SDK. Por exemplo: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Obtenha a ID do Roku para publicidade (RIDA) usando a API [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) do SDK do Roku. |

   <!--
    Roku Api Reference: 
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://docs.adobe.com/content/help/en/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
