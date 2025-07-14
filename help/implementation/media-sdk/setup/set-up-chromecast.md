---
title: Como configurar o SDK de mídia para Chromecast
description: Siga estas etapas para configurar o aplicativo do SDK de mídia no Chromecast.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 97%

---

# Configurar o SDK móvel v3.x para Chromecast {#set-up-chromecast}

Esta seção descreve os pré-requisitos para configurar uma instalação do Chromecast para a coleção de mídia de streaming.

## Pré-requisitos 

* **Obter parâmetros de configuração válidos**

  Estes parâmetros podem ser obtidos de um representante da Adobe após a configuração da conta de análise de mídia.
* **Inclua as seguintes APIs em seu player de mídia**

   * *Uma API para assinar eventos do player* - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * *Uma API que fornece informações sobre o player* - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

O Adobe Mobile Services fornece uma nova interface do usuário que reúne recursos de marketing móvel para aplicativos móveis de toda a Adobe Experience Cloud. Inicialmente, o Mobile Service fornece integração perfeita entre os recursos de análise e segmentação de aplicativos para as soluções do Adobe Analytics e do Adobe Target. Saiba mais pela [documentação do Adobe Mobile Services.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=pt-BR)

A biblioteca móvel da Adobe para Chromecast v3.x para soluções da Experience Cloud permite avaliar aplicativos de Chromecast criados com JavaScript, utilizar e coletar dados de públicos por meio do gerenciamento de públicos e medir o engajamento com o vídeo.

## Biblioteca móvel / Implementação do SDK

1. Adicione a biblioteca do Chromecast baixada ao projeto.

   1. O arquivo `AdobeMobileLibrary-Chromecast-[version]` zip consiste nos seguintes componentes de software:

      * `adbmobile-chromecast.min.js`:

        Esse arquivo de biblioteca será incluído na pasta de origem do aplicativo Chromecast.

      * Configuração `ADBMobileConfig`

        Esse arquivo de configuração do SDK foi personalizado para o aplicativo. Um exemplo de implementação de `ADBMobileConfig` é fornecido com o SDK (em `samples/`). Obtenha as configurações apropriadas de um representante da Adobe.

   1. Adicione o arquivo de biblioteca ao seu arquivo `index.html` e crie a variável global `ADBMobileConfig` da seguinte maneira (a variável global usada para configurar o Adobe Mobile para Media Analytics contém uma chave exclusiva denominada `mediaHeartbeat`):

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
              "rsids": "example.sample.player",
              "server": "example.sc.omtrc.net",
              "ssl": true,
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
              "server": "example.hb-api.omtrdc.net",
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg",
              "channel": "test-channel-chromecast",
              "ssl": true,
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
      >Se o `mediaHeartbeat` for configurado incorretamente, o módulo de mídia entrará em um estado de erro e deixará de enviar chamadas de rastreamento.

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

   O serviço de ID de visitante da Experience Cloud fornece uma ID de visitante universal nas soluções da Experience Cloud. O serviço de ID de visitante é exigido pelo Media Analytics e por outras integrações da Marketing Cloud.

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

   | Método | Descrição |
   | --- | --- |
   | `getMarketingCloudID()` | Recupera a ID de visitante da Experience Cloud do serviço de ID de visitante.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Com a ID de visitante da Experience Cloud, é possível definir outras IDs do cliente que podem ser associadas a cada visitante. A API de visitante aceita várias IDs de cliente para o mesmo visitante e um identificador de tipo de cliente para separar o escopo das diferentes IDs de clientes. Este método corresponde a `setCustomerIDs()` na biblioteca do JavaScript.  Por exemplo: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |

1. Para rastreamento de mídia, implemente o protocolo MediaDelegate

   ```js
    var delegate = {
      // Replace <currentPlaybackTime> with the video player current playback time
      getCurrentPlaybackTime = function() {
        return <currentPlaybackTime>;
      },
      // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.
      getQoSObject = function() {
         return ADBMobile.media.createQoSObject(<bitrate>, <startupTime>, <fps>, <droppedFrames>);
      }
    }
   
    ADBMobile.media.setDelegate(delegate);
   }
   ```

<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html?lang=pt-BR) -->
