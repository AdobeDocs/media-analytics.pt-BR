---
title: Como configurar o SDK de mídia para Roku
description: Siga estas etapas para configurar o aplicativo do SDK de mídia no Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 93%

---

# Configurar o SDK móvel v2.x para Roku {#set-up-roku}

## Pré-requisitos  {#roku-prerequisites}

* **Obter parâmetros de configuração válidos para o Complemento de Coleção de Mídia de Streaming**

  Esses parâmetros podem ser obtidos de um representante do Adobe após a configuração da conta do complemento Coleção de mídia de transmissão do Adobe.
* **Inclua as seguintes APIs em seu reprodutor de mídia**

   * _Uma API para assinar eventos do player_ - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * _Uma API que fornece informações sobre o player_ - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

O SDK 2.x do Roku para soluções da Experience Cloud permite avaliar aplicativos do Roku criados com BrightScript, utilizar e coletar dados de públicos por meio do gerenciamento de públicos e medir o engajamento com o vídeo através de eventos de vídeo.

## Biblioteca móvel / Implementação do SDK

1. Adicione a biblioteca [baixada](/help/getting-started/download-sdks.md) do Roku ao projeto.

   1. O arquivo de download `AdobeMobileLibrary-2.*-Roku.zip` consiste nos seguintes componentes de software:

      * `adbmobile.brs`: Esse arquivo de biblioteca será incluído na pasta de origem do aplicativo Roku.

      * `ADBMobileConfig.json`: Esse arquivo de configuração do SDK foi personalizado para o aplicativo.

   1. Adicione o arquivo da biblioteca e o arquivo de configuração JSON à origem do projeto.

      O JSON usado para configurar o Adobe Mobile tem uma chave exclusiva para o Media Analytics chamada `mediaHeartbeat`. Os parâmetros de configuração do Media Analytics pertencem a essa chave.

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
          "ssl":true,
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
         "ssl":true,
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

   O serviço de ID de visitante da Experience Cloud fornece uma ID de visitante universal nas soluções da Experience Cloud. O serviço de ID de visitante é exigido pelos eventos de vídeo e por outras integrações da Marketing Cloud.

   Verifique se a sua configuração `ADBMobileConfig` contém a ID da organização da `marketingCloud`.

   ```
   "marketingCloud": {
       "org": "YOUR-MCORG-ID"
   }
   ```

   As IDs de organização da Experience Cloud identificam de forma exclusiva cada empresa de clientes na Adobe Experience Cloud e são semelhantes ao seguinte valor: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Certifique-se de incluir `@AdobeOrg`.

   Após a configuração ser concluída, uma ID de visitante da Experience Cloud é gerada e incluída em todas as ocorrências. Outras IDs de visitante, como `custom` e `automatically-generated`, continuam a ser enviadas com cada ocorrência.

   **Métodos do Serviço de ID de visitante da Experience Cloud**

   >[!TIP]
   >
   >Os métodos de ID de visitante da Experience Cloud apresentam o prefixo `visitor`.

   |  Método   | Descrição |
   | --- | --- |
   | `visitorMarketingCloudID` | Recupera a ID de visitante da Experience Cloud do serviço de ID de visitante.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Com a ID de visitante da Experience Cloud, é possível definir outras IDs do cliente que podem ser associadas a cada visitante. A API de visitante aceita várias IDs de cliente para o mesmo visitante e um identificador de tipo de cliente para separar o escopo das diferentes IDs de clientes. Este método corresponde a `setCustomerIDs`. Por exemplo: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Usado para definir a ID do Roku para publicidade (RIDA) no SDK. Por exemplo: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Obtenha a ID do Roku para publicidade (RIDA) usando a API [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) do SDK do Roku. |
   | `getAllIdentifiers` | Retorna uma lista de todos os identificadores armazenados pelo SDK, incluindo Analytics, Visitante, Audience Manager e Identificadores personalizados. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   **APIs públicas adicionais**

   **DebugLogging**

   |  Método   | Descrição |
   | --- | --- |
   | `setDebugLogging` | Usado para ativar ou desativar o log de depuração do SDK. <br/><br/>`ADBMobile().setDebugLogging(true)` |
   | `getDebugLogging` | Retorna true se o log de depuração estiver ativado.  <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   **PrivacyStatus**

   | Constante   | Descrição |
   | --- | --- |
   | `PRIVACY_STATUS_OPT_IN` | Constante a ser transmitida ao chamar setPrivacyStatus para aceitação. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN` |
   | `PRIVACY_STATUS_OPT_OUT` | Constante a ser transmitida ao chamar setPrivacyStatus para recusa. <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT` |

   |  Método   | Descrição |
   | --- | --- |
   | `setPrivacyStatus` | Define o status de privacidade no SDK.  <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | Obtém o status de privacidade atual definido no SDK.  <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   >[!IMPORTANT]
   >
   >Certifique-se de chamar a função `processMessages` e `processMediaMessages` no loop do evento principal a cada 250 ms, para garantir que o SDK envie os pings corretamente.

   |  Método   | Descrição |
   | --- | --- |
   | `processMessages` | Responsável por transmitir os eventos do Analytics ao SDK para serem manipulados.  <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | Responsável por transmitir os eventos de mídia ao SDK para serem manipulados. <br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
