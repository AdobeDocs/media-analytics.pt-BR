---
title: Rastreamento no SceneGraph (Roku)
description: Saiba como rastrear mídia com a estrutura de programação XML do Roku SceneGraph.
uuid: fa85e546-c79b-4df4-8c03-d6593fa296d5
exl-id: e428d3cd-dbc7-48bb-82ff-61b6b892884c
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/yaQY00G4Tz-rR-Vs--nQXJ05ruXyD3oUwP2BPyocYDM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 1168
ht-degree: 97%

---

# Roku - Rastreamento no SceneGraph {#tracking-in-scenegraph-roku}

## Introdução {#introduction}

Você pode usar a estrutura de programação XML do Roku SceneGraph para desenvolver aplicativos. Esta estrutura apresenta dois conceitos principais:

* Renderização do SceneGraph das telas do aplicativo
* Configuração XML das telas do SceneGraph

O SDK do Adobe Mobile para Roku foi escrito em BrightScript. O SDK usa muitos componentes que não estão disponíveis para um aplicativo em execução no SceneGraph (por exemplo, threads). Portanto, um desenvolvedor do aplicativo Roku que pretende usar a estrutura do SceneGraph não pode chamar as APIs do SDK do Adobe Mobile (as últimas são semelhantes às disponíveis nos aplicativos herdados do BrightScript).

## Arquitetura {#architecture}

Para adicionar suporte do SceneGraph ao SDK do AdobeMobile, a Adobe adicionou uma nova API que cria um conector bridge entre o SDK do AdobeMobile e `adbmobileTask`. O último é um nó do SceneGraph usado para a execução da API do SDK. (O uso do `adbmobileTask` é explicado em detalhes mais adiante neste documento.)

A ponte do conector foi projetada para funcionar da seguinte forma:

* A ponte retorna uma instância compatível com o SceneGraph do SDK do AdobeMobile. O SDK compatível com o SceneGraph tem todas as APIs que o SDK herdado expõe.
* Você usa as APIs do SDK do AdobeMobile no SceneGraph de uma forma muito semelhante à forma como usava as APIs herdadas.
* A ponte também expõe um mecanismo para acompanhar retornos de chamada para APIs que retornam alguns dados.

![](assets/SceneGraph_arch.png)

## Componentes {#components}

**Aplicativo SceneGraph:**

* Consume APIs `AdobeMobileLibrary` por meio das APIs do conector bridge do SceneGraph.
* Registra retornos de chamada de resposta em `adbmobileTask` para as variáveis de dados de saída esperadas.

**AdobeMobileLibrary:**

* Expõe um conjunto de APIs públicas (Herdadas), incluindo a API de ponte do conector.
* Retorna uma instância do conector do SceneGraph que envolve todas as APIs públicas herdadas.
* Comunica-se com um nó `adbmobileTask` do SceneGraph para a execução de APIs.

**Nó adbmobileTask:**

* Um nó de tarefa do SceneGraph que executa as APIs `AdobeMobileLibrary` em um thread em segundo plano.
* Atua como um representante para retornar os dados às cenas do aplicativo.

## APIs públicas do SceneGraph {#public-scenegraph-apis}

### ADBMobileConnector

| Categoria | Nome do método | Descrição |
|---|---|---|
| **Constantes** | |  |
|  | `sceneGraphConstants` | Retorna um objeto contendo `SceneGraphConstants`. Consulte os detalhes na tabela acima. |
|  | | |
| **Registro de depuração** | | |
|  | `setDebugLogging` | API do SceneGraph para definir o log de depuração no SDK do ADBMobile. |
|  | `getDebugLogging` | API do SceneGraph para obter o log de depuração do SDK do ADBMobile. |
|  | Para obter mais informações, consulte a seção Log de depuração do SDK herdado. | |
|  | | |
| **Status de privacidade / Rejeição** | | |
|  | `setPrivacyStatus` | API do SceneGraph para definir o status de privacidade no SDK do ADBMobile. |
|  | `getPrivacyStatus` | API do SceneGraph para obter o status de privacidade do SDK do ADBMobile. |
|  | Para obter mais informações, consulte a seção Status de exclusão/privacidade do SDK herdado. | |
|  | | |
| **Analytics** | | |
|  | `trackState` | API do SceneGraph para rastrear o estado no SDK do ADBMobile. |
|  | `trackAction` | API do SceneGraph para rastrear ações no SDK do ADBMobile. |
|  | `trackingIdentifier` | API do SceneGraph para obter um identificador de rastreamento do SDK do ADBMobile. |
|  | `userIdentifier` | API do SceneGraph para obter um identificador do usuário do SDK do ADBMobile. |
|  | `setUserIdentifier` | API do SceneGraph para definir o identificador do usuário no SDK do ADBMobile. |
|  | `getAllIdentifiers` | A API do SceneGraph recupera todas as identidades de usuário conhecidas e persistentes pelo SDK Roku. |
|  | Para obter mais informações, consulte a seção Analytics do SDK herdado. | |
|  | | |
| **Experience Cloud** | | |
|  | `visitorSyncIdentifiers` | API do SceneGraph para sincronizar os identificadores da Experience Cloud no SDK do ADBMobile. |
|  | `visitorMarketingCloudID` | API do SceneGraph para obter a ID de visitante da Experience Cloud ID do SDK do ADBMobile. |
|  | Para obter mais informações, consulte a seção Experience Cloud do SDK herdado. | |
|  | | |
| **Audience Manager** | | |
|  | `audienceSubmitSignal` | API do SceneGraph para enviar um sinal de gerenciamento de público-alvo com características. |
|  | `audienceVisitorProfile` | API do SceneGraph para obter um perfil de visitante do Audience Manager do SDK do ADBMobile. |
|  | `audienceDpid` | API do SceneGraph para obter um Dpid de público-alvo do SDK do ADBMobile. |
|  | `audienceDpuuid` | API do SceneGraph para obter um Dpuuid de público-alvo do SDK do ADBMobile. |
|  | `audienceSetDpidAndDpuuid` | API do SceneGraph para definir o Dpid e o Dpuuid de público-alvo no SDK ADBMobile. |
|  | Para obter mais informações, consulte a seção Audience Manager do SDK herdado. | |
|  | | |
| **MediaHeartbeat** | | |
|  | `mediaTrackLoad` | API do SceneGraph para carregar conteúdo de vídeo para o rastreamento de MediaHeartbeat. |
|  | mediaTrackStart | API do SceneGraph para iniciar a sessão de rastreamento de vídeo usando o MediaHeartbeat. |
|  | `mediaTrackUnload` | API do SceneGraph para descarregar conteúdo de vídeo do rastreamento de MediaHeartbeat. |
|  | `mediaTrackPlay` | API do SceneGraph para rastrear a reprodução do conteúdo de vídeo. |
|  | mediaTrackPause | API do SceneGraph para rastrear conteúdo de vídeo pausado. |
|  | `mediaTrackComplete` | API do SceneGraph para rastrear a conclusão da reprodução do conteúdo de vídeo. |
|  | `mediaTrackError` | API do SceneGraph para rastrear erros de reprodução. |
|  | mediaTrackEvent | API do SceneGraph para rastrear eventos de reprodução durante o rastreamento. Por exemplo: Anúncios, capítulos. |
|  | `mediaUpdatePlayhead` | API do SceneGraph para enviar atualizações de indicador de reprodução ao MediaHeartbeat durante o rastreamento de vídeo. |
|  | `mediaUpdateQoS` | API do SceneGraph para enviar atualizações de QoS ao MediaHeartbeat durante o rastreamento de vídeo. |
|  | Para obter mais informações, consulte a seção MediaHeartbeat do SDK herdado. | |

### SceneGraphConstants

| Nome da constante | Descrição |
|---|---|
| `API_RESPONSE` | Usado para recuperar o objeto de resposta do campo `adbmobileTask` do nó `adbmobileApiResponse` |
| `DEBUG_LOGGING` | Usado como `apiName` para `getDebugLogging` |
| `PRIVACY_STATUS` | Usado como `apiName` para `getPrivacyStatus` |
| `TRACKING_IDENTIFIER` | Usado como `apiName` para `trackingIdentifier` |
| `USER_IDENTIFIER` | Usado como `apiName` para `userIdentifier` |
| `VISITOR_MARKETING_CLOUD_ID` | Usado como `apiName` para `visitorMarketingCloudID` |
| `AUDIENCE_VISITOR_PROFILE` | Usado como `apiName` para `audienceVisitorProfile` |
| `AUDIENCE_DPID` | Usado como `apiName` para `audienceDpid` |
| `AUDIENCE_DPUUID` | Usado como `apiName` para `audienceDpuuid` |

### Nó adbmobileTask

<table>
<thead>
<tr>
<td> Campo </td><td> Tipo </td><td> Padrão </td><td> Uso </td>
</tr>
</thead>
<tbody>
<tr>
<td> adbmobileApiCall </td>
<td> assocarray </td>
<td> Inválido </td>
<td> NÃO modifique este campo nem permita que seja utilizado pelo Aplicativo. Este campo é usado pelo ADBMobile SceneGraphConnector para rotear as chamadas de API por meio dos nós do SceneGraph e obter as respostas. Portanto, essa chave/campo é reservada para AdobeMobileSDK para compatibilidade com o SceneGraph. <b>Importante:</b> qualquer modificação nesse campo pode resultar no funcionamento incorreto do AdobeMobileSDK.</td>
</tr>
<tr>
<td> adbmobileApiResponse </td>
<td> assocarray </td>
<td> Inválido </td>
<td> Somente leitura. Todas as APIs executadas no AdobeMobileSDK retornarão respostas neste campo. Registre-se para um retorno de chamada para detectar as atualizações desse campo e receber objetos de resposta. A seguir está o formato para o objeto de resposta:  
<pre>
resposta = {
  "apiName" : &lt;SceneGraphConstants.
               API_NAME&gt;
  "returnValue : &lt;API_RESPONSE&gt;
}</pre>
Uma instância desse objeto de resposta será enviada para qualquer chamada de API no AdobeMobileSDK que deveria retornar um valor de acordo com o guia de referência da API. Por exemplo, uma chamada de API para visitorMarketingCloudID() retornará o seguinte objeto de resposta:
<pre>
resposta = {
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : "07050x25671x33760x72644x14"  
}
</pre>
OU, os dados de resposta também podem ser inválidos:
<pre>
resposta = {  
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : inválido
}
</pre>
</td>
</tr>
</tbody>
</table>

### `adbmobile.brs`

#### `getADBMobileConnectorInstance`

Assinatura da API: `ADBMobile().getADBMobileConnectorInstance()`\
Entrada: `adbmobileTask`
Tipo de Retorno: `ADBMobileConnector`

#### `sgConstants`

Assinatura da API: `ADBMobile().sgConstants()`
Entrada: Nenhum\
Tipo de retorno: `SceneGraphConstants`

>[!NOTE]
>Consulte a referência da API `ADBMobileConnector` para obter mais detalhes.

### Constantes do ADBMobile

|  Recurso  | Nome da constante | Descrição   |
|---|---|---|
| Controle de versão | `version` | Constante para recuperar informações de versão do AdobeMobileLibrary |
| Privacidade/opção de não participação | `PRIVACY_STATUS_OPT_IN` | Constante para o status de privacidade aceito |
|   | `PRIVACY_STATUS_OPT_OUT` | Constante para o status de privacidade não aceito |
| Constantes do MediaHeartbeat | Consulte as constantes nesta página: <br/><br/>[Métodos de heartbeat de mídia.](/help/use-cases/track-av-playback/track-core/track-core-roku.md) | Use essas constantes com as APIs do MediaHeartbeat |
| Metadados padrão | Consulte as constantes nesta página: <br/><br/>[Parâmetros de metadados padrão.](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md) | Use essas constantes para anexar metadados de vídeo/anúncio padrão às APIs do MediaHeartbeat |



As APIs do `MediaHeartbeat` definidas globalmente na AdobeMobileLibrary herdada podem ser acessadas *como estão* no ambiente do SceneGraph porque elas não usam componentes do Brightscript que não estejam disponíveis nos nós do SceneGraph. Para obter mais informações sobre esses métodos, consulte a tabela abaixo:

### Métodos globais para MediaHeartbeat

| Método | Descrição |
| --- | --- |
| `adb_media_init_mediainfo` | Esse método retorna um objeto de Informações de mídia inicializado. `Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object` |
| `adb_media_init_adinfo` | Este método retorna o objeto de Informações do anúncio. `Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object` |
| `adb_media_init_chapterinfo` | Este método retorna o objeto de Informações do capítulo inicializado. `Function adb_media_init_adbreakinfo(name As String, startTime as Double, position as Double) As Object` |
| `adb_media_init_adbreakinfo` | Este método retorna o objeto de Informações do AdBreak inicializado. `Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object` |
| `adb_media_init_qosinfo` | Este método retorna um objeto de Informações de QoS inicializado. `Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object` |

## Implementação {#implementation}

1. **Baixe a biblioteca do Roku -** Baixe a [biblioteca do Roku mais recente.](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.2)

1. **Configurar o ambiente de desenvolvimento**

   1. Copie `adbmobile.brs` (AdobeMobileLibrary) no diretório `pkg:/source/`.

   1. Para obter suporte ao SceneGraph, copie `adbmobileTask.brs` e `adbMobileTask.xml` no diretório `pkg:/components/`.

1. **Inicializar**

   1. Importe `adbmobile.brs` na cena.

      ```
      <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
      ```

   1. Crie uma instância do nó `adbmobileTask` na Cena.

      ```
      m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
      ```

   1. Obtenha uma instância do conector `adbmobile` para o SceneGraph usando a instância `adbmobileTask`.

      ```
      m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
      ```

   1. Obtenha as constantes `adbmobile` do SG.

      ```
      m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
      ```

   1. Registre um retorno de chamada para receber o objeto de resposta para todas as chamadas de API `AdbMobile`.

      ```
      m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE,  
                                   "onAdbmobileApiResponse")
      
      ' Sample implementation of the callback
      ' Listen for all the constants for which API calls are made on the SDK
      function onAdbmobileApiResponse() as void
          responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
      
          if responseObject <> invalid
              methodName = responseObject.apiName
              retVal = responseObject.returnValue
      
              if methodName = m.adbmobileConstants.DEBUG_LOGGING
                  if retVal
                      print "API Response: DEBUG LOGGING: " + "True"
                  else
                      print "API Response: DEBUG LOGGING: " + "False"
                  endif
              else if methodName = m.adbmobileConstants.PRIVACY_STATUS
                  print "API Response: PRIVACY STATUS: " + retVal
              else if methodName = m.adbmobileConstants.TRACKING_IDENTIFIER
                  if retVal <> invalid
                      print "API Response: TRACKING IDENTIFIER: " + retVal
                  else
                      print "API Response: TRACKING IDENTIFIER: " + "invalid"
                  endif
              else if methodName = m.adbmobileConstants.USER_IDENTIFIER
                  if retVal <> invalid
                      print "API Response: USER IDENTIFIER: " + retVal
                  else
                      print "API Response: USER IDENTIFIER: " + "invalid"
                  endif
              else if methodName = m.adbmobileConstants.VISITOR_MARKETING_CLOUD_ID
                  if retVal <> invalid
                      print "API Response: MCID: " + retVal
                  else
                      print "API Response: MCID: " + "invalid"
                  endif
              else if methodName = m.adbmobileConstants.AUDIENCE_DPID
                  if retVal <> invalid
                      print "API Response: AUDIENCE DPID: " + retVal
                  else
                      print "API Response: AUDIENCE DPID: " + "invalid"
                  endif
              else if methodName = m.adbmobileConstants.AUDIENCE_DPUUID
                  if retVal <> invalid
                      print "API Response: AUDIENCE DPUUID: " + retVal
                  else
                      print "API Response: AUDIENCE DPUUID: " + "invalid"
                  endif
              else if methodName = m.adbmobileConstants.AUDIENCE_VISITOR_PROFILE
                  if retVal <> invalid
                      print "API Response: AUDIENCE VISITOR PROFILE: Valid Object"
                  else
                      print "API Response: AUDIENCE VISITOR PROFILE: " + "invalid"
                  endif
              endif
          endif
      end function
      ```

## Exemplo de implementação {#sample-implementation}

### Exemplos de chamadas de API no SDK herdado

```
'get an instance of SDK
m.adbmobile = ADBMobile()

'execute setter APIs
m.adbmobile.setDebugLogging(true)

'execute getter APIs
debugLogging = m.adbmobile.getDebugLogging()
```

### Exemplos de chamadas de API no SDK do SG

```
'create adbmobileTask instance
m.adbmobileTask = createObject("roSGNode", "adbmobileTask")

'get an instance of SDK using task instance
m.adbmobile =  
  ADBMobile().getADBMobileConnectorInstace(m.adbmobileTask)
m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
'execute setter APIs
m.adbmobile.setDebugLogging(true)

'execute getter APIs
m.adbmobileTask.ObserverField(m.adbConstants.API_RESPONSE,  
                              "onAdbmobileApiResponse")
m.adbmobile.getDebugLogging()

'listen for return data in registered callbacks
function onAdbmobileApiResponse() as void
    responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]

        if responseObject <> invalid
            methodName = responseObject.apiName
            retVal = responseObject.returnValue

        if methodName = m.adbmobileConstants.DEBUG_LOGGING
            if retVal
                print "API Response: DEBUG LOGGING: " + "True"
            else
                print "API Response: DEBUG LOGGING: " + "False"
         endif
    endif
end function
```
