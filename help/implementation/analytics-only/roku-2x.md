---
title: Configurar o Roku 2.x para mídia de transmissão
description: Instale e configure o Adobe Media SDK 2.x para Roku para implementações de mídia de transmissão exclusivas do Analytics, incluindo canais do SceneGraph.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---

# Configurar o Roku 2.x para mídia de transmissão

O Adobe Media SDK 2.x para Roku (`adbmobile.brs`) envia dados de mídia de transmissão dos canais Roku escritos em BrightScript diretamente para o Adobe Analytics. Ele também coleta dados do público-alvo por meio do Audience Manager e mede o engajamento por meio de eventos de mídia.

>[!NOTE]
>
>Esta página aborda o Media SDK 2.x somente para análise para Roku. Para novas implementações, a Adobe recomenda o [Roku Edge SDK](/help/implementation/edge/roku.md), que disponibiliza dados para o Customer Journey Analytics, o Adobe Journey Optimizer e o Real-Time CDP, além do Adobe Analytics.

* **Pré-requisitos**:
   * Conclua a [visão geral da implementação somente do Analytics](overview.md).
   * [Baixe o Media SDK para Roku](/help/getting-started/download-sdks.md).
   * Inclua uma API no reprodutor de mídia para assinar eventos do reprodutor e uma API que forneça informações do reprodutor, como o nome da mídia e a posição do indicador de reprodução.

## Instalar o SDK

O download de `AdobeMobileLibrary-2.*-Roku.zip` contém dois componentes:

* `adbmobile.brs`: o arquivo da biblioteca. Copie-o no diretório `pkg:/source/` do seu canal.
* `ADBMobileConfig.json`: o arquivo de configuração do SDK, personalizado para o seu aplicativo.

Para os canais do SceneGraph, copie também `adbmobileTask.brs` e `adbmobileTask.xml` no diretório `pkg:/components/`. Consulte [suporte a SceneGraph](#scenegraph).

## Configurar ADBMobileConfig.json

O JSON de configuração tem uma chave `mediaHeartbeat` exclusiva para streaming de mídia. Adicione `ADBMobileConfig.json` à origem do projeto e defina os valores de `mediaHeartbeat`, `marketingCloud` e `analytics`:

```json
{
  "analytics": {
    "rsids": "your-report-suite-id",
    "server": "your-analytics-server"
  },
  "marketingCloud": {
    "org": "YOUR-MCORG-ID@AdobeOrg"
  },
  "mediaHeartbeat": {
    "server": "your-namespace.hb-api.omtrdc.net",
    "publisher": "your-publisher-id",
    "channel": "sample-channel",
    "ssl": true,
    "ovp": "sample-ovp",
    "sdkVersion": "sample-sdk",
    "playerName": "Roku Player"
  }
}
```

| Parâmetro de configuração | Descrição |
| --- | --- |
| `server` | URL do endpoint de rastreamento de mídia. Consulte a [visão geral da implementação somente do Analytics](overview.md). |
| `publisher` | Identificador exclusivo do publicador de conteúdo. |
| `channel` | Nome do canal de distribuição de conteúdo. Relatado como [Canal de conteúdo](/help/implementation/variables/core/content-channel.md). |
| `ssl` | Se o SSL é usado para chamadas de rastreamento. |
| `ovp` | Nome do provedor da plataforma de vídeo online. |
| `sdkVersion` | Versão atual do aplicativo ou SDK. |
| `playerName` | Nome do reprodutor. Relatado como [Nome do player de conteúdo](/help/implementation/variables/core/content-player-name.md). |

>[!IMPORTANT]
>
>Se `mediaHeartbeat` estiver configurado incorretamente, o módulo de mídia entrará em um estado de erro e parará de enviar chamadas de rastreamento. Verifique se o valor `marketingCloud.org` inclui `@AdobeOrg`.

## Inicializar o SDK e processar mensagens

Obtenha uma instância da SDK com `ADBMobile()`. O serviço de ID de visitante da Experience Cloud gera uma ID de visitante que está incluída em todas as ocorrências.

>[!IMPORTANT]
>
>Chame `processMessages` e `processMediaMessages` no loop do evento principal a cada 250 ms para que o SDK envie pings corretamente.

```brightscript
adb = ADBMobile()

' In your main event loop, every ~250 ms:
adb.processMessages()
adb.processMediaMessages()
```

| Método | Descrição |
| --- | --- |
| `processMessages` | Passa eventos do Analytics em fila para o SDK. |
| `processMediaMessages` | Passa eventos de mídia enfileirados para o SDK, incluindo pings automáticos. |

## Rastrear eventos de mídia

Rastreie cada evento de mídia chamando seu método SDK. Consulte a guia **Roku 2.x** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as chamadas, construtores e constantes exatas.

Uma sessão típica começa criando um objeto de mídia e chamando `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Mr. Robot", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

contextData = { "a.media.show": "Mr. Robot" }

adb.mediaTrackSessionStart(mediaInfo, contextData)
```

Os construtores globais `adb_media_init_*` criam os objetos de mídia, anúncio, ad-break, capítulo e QoS usados pelas chamadas de rastreamento:

| Construtor | Assinatura |
| --- | --- |
| Mídia | `adb_media_init_mediainfo(name, id, length, streamType, mediaType)` |
| Publicidade | `adb_media_init_adinfo(name, id, position, length)` |
| Quebra do anúncio | `adb_media_init_adbreakinfo(name, startTime, position)` |
| Capítulo | `adb_media_init_chapterinfo(name, position, length, startTime)` |
| QoS | `adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)` |

Os metadados padrão são passados como uma matriz associativa de `a.media.*` chaves (o SDK também define constantes nomeadas, como `MEDIA_VideoMetadataKeySHOW`, para essas chaves). Consulte as páginas [Variáveis](/help/implementation/variables/overview.md) para a chave que corresponde a cada dimensão.

## Configurar a ID de visitante, a privacidade e o registro da Experience Cloud

Os métodos a seguir na instância `ADBMobile()` gerenciam identidade, privacidade e depuração:

| Método | Descrição |
| --- | --- |
| `visitorMarketingCloudID()` | Recupera a Experience Cloud ID (ECID). |
| `visitorSyncIdentifiers(identifiers)` | Define outras IDs do cliente para o mesmo visitante. |
| `setAdvertisingIdentifier(rida)` | Define a ID do Roku para o Advertising (RIDA). Obtenha-o com a API do Roku [`getRIDA()`](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic). |
| `getAllIdentifiers()` | Retorna todos os identificadores armazenados pela SDK, incluindo Analytics, Visitante, Audience Manager e identificadores personalizados. |
| `setPrivacyStatus(status)` | Define o status de privacidade. Aprovado `adb.PRIVACY_STATUS_OPT_IN` ou `adb.PRIVACY_STATUS_OPT_OUT`. Consulte [Privacidade](/help/implementation/opt-out-privacy.md). |
| `getPrivacyStatus()` | Retorna o status de privacidade atual. |
| `setDebugLogging(flag)` | Ativa ou desativa o log de depuração. |
| `getDebugLogging()` | Retorna `true` se o log de depuração estiver habilitado. |

## Suporte ao SceneGraph {#scenegraph}

A estrutura XML do Roku SceneGraph não pode chamar as APIs herdadas do BrightScript SDK diretamente, pois o SDK usa componentes (como threads) que não estão disponíveis para um aplicativo SceneGraph. Para preencher essa lacuna, o SDK fornece um conector que retorna uma instância compatível com o SceneGraph expondo as mesmas APIs, além de um mecanismo de retorno de chamada para APIs que retornam dados.

A ponte tem três partes:

* **`adbmobileTask`nó**: um nó de tarefa do SceneGraph que executa as APIs do SDK em um thread em segundo plano e retorna os dados às suas cenas.
* **Instância do conector**: envolve todas as APIs públicas herdadas e se comunica com o nó `adbmobileTask`.
* **`API_RESPONSE`retorno de chamada**: o campo que seu aplicativo observa para receber valores de retorno de APIs getter.

Para inicializar o SDK em um canal do SceneGraph:

1. Importar `adbmobile.brs` para sua cena:

   ```brightscript
   <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
   ```

1. Crie o nó `adbmobileTask`, obtenha a instância do conector e carregue as constantes do SceneGraph:

   ```brightscript
   m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
   m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
   m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
   ```

1. Registre um retorno de chamada para receber objetos de resposta para APIs que retornam dados:

   ```brightscript
   m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE, "onAdbmobileApiResponse")
   
   function onAdbmobileApiResponse() as void
       responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
       if responseObject <> invalid
           methodName = responseObject.apiName
           retVal = responseObject.returnValue
           if methodName = m.adbmobileConstants.PRIVACY_STATUS
               print "Privacy status: " + retVal
           end if
       end if
   end function
   ```

A instância do conector (`m.adbmobile`) expõe os mesmos métodos de mídia que o SDK herdado (`mediaTrackSessionStart`, `mediaTrackPlay`, `mediaTrackPause`, `mediaTrackComplete`, `mediaTrackSessionEnd`, `mediaTrackError`, `mediaTrackEvent`, `mediaUpdatePlayhead` e `mediaUpdateQoS`), de modo que as chamadas mostradas nas páginas de evento e variável funcionam da mesma forma. As APIs setter são chamadas diretamente; as APIs getter retornam seus valores por meio do retorno de chamada `API_RESPONSE`.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações somente do Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
>* [Visão geral das variáveis](/help/implementation/variables/overview.md)
>* [Roku Edge SDK](/help/implementation/edge/roku.md)
