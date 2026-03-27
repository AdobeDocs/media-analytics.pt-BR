---
title: Parâmetros de solicitação de � da API de serviços de mídia de streaming
description: Quais são os parâmetros de solicitação da API Media Collection, as chaves de solicitação e as descrições.
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 528a82a4299370c2ef5a366b1f3fab9fd21b164f
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 96%

---

# Parâmetros da solicitação{#request-parameters}

## Dados do Analytics

| Chave da solicitação  | Obrigatório | Chave de tipo de solicitação | Definir em... |  Descrição  |
| --- | :---: | :---: | :---: | --- |
| `analytics.trackingServer` | S | string | `sessionStart` | O URL do servidor do Adobe Analytics. |
| `analytics.reportSuite` | S | string | `sessionStart` | A ID que identifica os dados de relatórios do Analytics |
| `analytics.enableSSL` | N | booleano | `sessionStart` | True ou false para habilitar o SSL |
| `analytics.visitorId` | N | string | `sessionStart` | A ID de visitante da Adobe é uma ID personalizada que você pode usar em vários aplicativos da Adobe. O `visitorId` do Heartbeat é igual ao `VID.` do Analytics |

## Dados do visitante

| Chave da solicitação  | Obrigatório | Chave de tipo de solicitação | Definir em... |  Descrição  |
| --- | :---: | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | S | string | `sessionStart` | A ID da organização da Experience Cloud identifica sua organização no sistema da Adobe Experience Cloud |
| `visitor.marketingCloudUserId` | N | string | `sessionStart` | Esta é a ID de usuário da Experience Cloud (ECID). Na maioria dos casos, essa é a ID que você deve usar para identificar um usuário. O `marketingCloudUserId` do Heartbeat é igual ao `MID` no Adobe Analytics. Embora não seja tecnicamente necessário, esse parâmetro é necessário para acessar a família de aplicativos da Experience Cloud. |
| `visitor.aamLocationHint` | N | inteiro | `sessionStart` | Fornece dados de borda do Adobe Audience Manager. Se um valor não for inserido, ele será nulo. |
| `appInstallationId` | N | string | `sessionStart` | O appInstallationId identifica exclusivamente o aplicativo e o dispositivo |

## Dados de conteúdo

| Chave da solicitação  | Obrigatório | Chave de tipo de solicitação | Definir em... |  Descrição  |
| --- | :---: | :---: | :---: | --- |
| `media.id` | S | string | `sessionStart` | Identificador exclusivo para o conteúdo |
| `media.name` | N | string | `sessionStart` | Nome legível para o conteúdo |
| `media.length` | S | number | `sessionStart` | Duração do conteúdo (segundos) |
| `media.contentType` | S | string | `sessionStart` | Formato do fluxo (pode ser qualquer sequência de caracteres. Alguns valores recomendados são &quot;Live&quot;, &quot;VOD&quot; ou &quot;Linear&quot;) |
| `media.playerName` | S | string | `sessionStart` | O nome do reprodutor responsável pela renderização do conteúdo |
| `media.channel` | S | string | `sessionStart` | O canal de distribuição do conteúdo. Pode ser um nome de aplicativo móvel ou um nome de site, nome de propriedade |
| `media.resume` | N | booleano | `sessionStart` | Indica se um usuário está ou não retomando uma sessão anterior (em vez de iniciar uma nova sessão) |
| `media.sdkVersion` | N | string | `sessionStart` | A versão de SDK usada pelo reprodutor |

## Metadados padrão de conteúdo

| Chave da solicitação  | Obrigatório | Chave de tipo de solicitação | Definir em... |  Descrição  |
| --- | :---: | :---: | :---: | --- |
| `media.streamFormat` | N | string | `sessionStart` | Formato do streaming; por exemplo, “HD” |
| `media.show` | N | string | `sessionStart` | O nome do programa ou da série |
| `media.season` | N | string | `sessionStart` | O número da temporada do programa ou da série |
| `media.episode` | N | string | `sessionStart` | O número do episódio |
| `media.assetId` | N | string | `sessionStart` | O identificador exclusivo para o conteúdo do material de vídeo, como o identificador de episódio da série de TV, identificador de material de filme ou identificador de evento ao vivo. Normalmente, essas IDs são derivadas de autoridades de metadados, como EIDR, TMS/Gracenote ou Rovi. Esses identificadores também podem ser de outros sistemas proprietários ou internos. |
| `media.genre` | N | string | `sessionStart` | O tipo de conteúdo conforme definido pelo produtor do conteúdo |
| `media.firstAirDate` | N | string | `sessionStart` | A data quando o conteúdo foi exibido na televisão pela primeira vez |
| `media.firstDigitalDate` | N | string | `sessionStart` | A data quando o conteúdo foi exibido em qualquer plataforma digital pela primeira vez |
| `media.rating` | N | string | `sessionStart` | A classificação conforme definido pelas Diretrizes de controle parental da TV |
| `media.originator` | N | string | `sessionStart` | O criador do conteúdo |
| `media.network` | N | string | `sessionStart` | O nome da rede/canal |
| `media.showType` | N | string | `sessionStart` | O tipo de conteúdo, expresso como um número inteiro entre 0 e 3: <ul> <li>0 - Episódio completo </li> <li>1 - Visualização </li> <li>2 - Clip </li> <li>3 - Outro </li> </ul> |
| `media.adLoad` | N | string | `sessionStart` | O tipo de anúncio carregado |
| `media.pass.mvpd` | N | string | `sessionStart` | O MVPD fornecido pela autenticação da Adobe |
| `media.pass.auth` | N | string | `sessionStart` | Indica que o usuário foi autorizado pela autenticação da Adobe (só pode ser true se estiver definido) |
| `media.dayPart` | N | string | `sessionStart` | A hora do dia em que o conteúdo foi transmitido |
| `media.feed` | N | string | `sessionStart` | O tipo de feed, por exemplo, &quot;West-HD&quot; |

## Dados de publicidade

| Chave da solicitação  | Obrigatório | Chave de tipo de solicitação | Definir em... |  Descrição  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | string | `adBreakStart` | O nome amigável do ad break |
| `media.ad.podIndex` | S | inteiro | `adBreakStart` | O índice do pod de anúncios no vídeo |
| `media.ad.podSecond` | S | number | `adBreakStart` | O segundo em que o pod iniciou |
| `media.ad.podPosition` | S | inteiro | `adStart` | O índice do anúncio dentro do ad break que começa em 1 |
| `media.ad.name` | N | string | `adStart` | Nome amigável do anúncio |
| `media.ad.id` | S | string | `adStart` | O nome do anúncio |
| `media.ad.length` | S | number | `adStart` | A duração do anúncio de vídeo em segundos |
| `media.ad.playerName` | S | string | `adStart` | O nome do reprodutor responsável pela renderização do anúncio |

## Metadados de publicidade padrão

| Chave da solicitação  | Obrigatório | Chave de tipo de solicitação | Definir em... |  Descrição  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.advertiser` | N | string | `adStart` | A empresa ou marca cujo produto aparece no anúncio |
| `media.ad.campaignId` | N | string | `adStart` | A ID da campanha publicitária |
| `media.ad.creativeId` | N | string | `adStart` | A ID de criação do anúncio |
| `media.ad.siteId` | N | string | `adStart` | A ID do site do anúncio |
| `media.ad.creativeURL` | N | string | `adStart` | O URL da arte do anúncio |
| `media.ad.placementId` | N | string | `adStart` | A ID de posicionamento do anúncio |

## Dados do capítulo

| Chave da solicitação  | Obrigatório | Chave de tipo de solicitação | Definir em... |  Descrição  |
| --- | :---: | :---: | :---: | --- |
| `media.chapter.index` | S | inteiro | `chapterStart` | Identifica a posição do capítulo no conteúdo |
| `media.chapter.offset` | S | number | `chapterStart` | O segundo na reprodução em que o capítulo inicia |
| `media.chapter.length` | S | number | `chapterStart` | A duração do capítulo em segundos. |
| `media.chapter.friendlyName` | N | string | `chapterStart` | O nome amigável do capítulo |

## Dados de qualidade

| Chave da solicitação  | Obrigatório | Chave de tipo de solicitação | Definir em... |  Descrição  |
| --- | :---: | :---: | :---: | --- |
| `media.qoe.bitrate` | N | inteiro | Qualquer | A taxa média de bits (em bps). A taxa média de bits é calculada como uma média ponderada de todos os valores de taxa de bits relacionados à duração da reprodução ocorridos durante a sessão de reprodução. |
| `media.qoe.droppedFrames` | N | inteiro | Qualquer | O número de quadros soltos na transmissão |
| `media.qoe.framesPerSecond` | N | inteiro | Qualquer | O número de quadros por segundo |
| `media.qoe.timeToStart` | N | inteiro | Qualquer | O tempo (em milissegundos) decorrido entre o momento em que o usuário aperta o play e o conteúdo é carregado e começa a ser reproduzido. |

## Parâmetros da Lei de Privacidade do Consumidor da Califórnia (CCPA) {#ccpa-params}

| Chave da solicitação  | Obrigatório | Chave de tipo de solicitação | Definir em... |  Descrição  |
| --- | :---: | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | booleano | `sessionStart` | Definido como true quando o usuário final optou por não ter os dados compartilhados entre o Adobe Analytics e outras soluções da Experience Cloud (por exemplo, Audience Manager) |
| `analytics.optOutShare` | N | booleano | `sessionStart` | Definido como true quando o usuário final optou por não ter seus dados federados (por exemplo, para outros clientes do Adobe Analytics). |

## Detalhes adicionais {#additional-details}

### visitor.marketingCloudUserId

Passe a ID de usuário da Experience Cloud (também conhecida como `MID` ou `MCID`) na chamada de `sessionStart`, ao inclui-la no mapa `params` usando a seguinte chave: **visitor.marketingCloudUserId**. Esse é um recurso útil se você já estiver integrado a outros produtos da Experience Cloud e tiver obtido o MCID.

>[!NOTE]
>
>O Media Analytics (MA) é integrado à família de aplicativos da Experience Cloud (Adobe Analytics, Audience Manager, Target, etc.). Você precisa de uma Experience Cloud ID para acessar esses aplicativos. _A ECID é o que você deve usar para identificar usuários na maioria dos cenários._

### appInstallationId

* **Se você *não* passar um `appInstallationId` valor -** O back-end do MA não gerará mais um MCID, mas dependerá do Adobe Analytics para fazer isso. A recomendação da Adobe é enviar um MCID, se disponível, ou um `appInstallationId` (juntamente com o `marketingCloudOrgId` ainda obrigatório), para que a API da coleção de mídia gere o MCID e o envie em todas as chamadas.

* **Se você *passar* o `appInstallationId` valor -** O MCID *pode ser* gerado pelo back-end do MA, se você passar valores para os parâmetros `appInstallationId` e o `marketingCloudOrgId` (obrigatório). Se você passar `appInstallationId`, deverá manter o seu valor no lado do cliente. Ele deve ser exclusivo para o aplicativo em um dispositivo e ser mantido enquanto o aplicativo não for reinstalado.

>[!NOTE]
>
>O `appInstallationId` identifica exclusivamente o aplicativo *e o dispositivo*. Ele precisa ser exclusivo para cada aplicativo em cada dispositivo, ou seja, dois usuários usando a mesma versão do mesmo aplicativo em diferentes dispositivos devem enviar um `appInstallationId` diferente (exclusivo), separadamente.

<!-- 
Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> 
-->

### visitor.marketingCloudOrgId

Além de ser necessário para a geração do MCID quando isso não for fornecido, esse parâmetro também será usado como o valor da ID do publicador (baseado na forma como ao Media Analytics realiza a [correspondência de regras de federação.](/help/use-cases/federated-media.md))

### ID do usuário herdada do Analytics (aid) e IDs do usuário declaradas (customerIDs)

* **analytics.aid:**

  o valor dessa chave deve ser uma sequência de caracteres que representa ID do usuário herdada do Analytics
* **visitor.customerIDs:**

  o valor dessa chave deve ser um objeto com o seguinte formato:

  ```js
  "<<insert your ID name here>>": {  
    "id": " <<insert your id here>>",  
     "authState": <<insert one of 0, 1, 2>>
  }
  ```

Observe que o valor `visitor.customerIDs` pode ter qualquer número de objetos no formato apresentado.

### visitor.aamLocationHint

Este parâmetro indica qual a borda do Adobe Audience Manager (AAM) terá uma ocorrência quando o Adobe Analytics enviar os dados do cliente para o Audience Manager. Se um valor não for inserido, ele será nulo. Isso é particularmente importante quando os usuários finais tendem a usar seus dispositivos em locais geograficamente distantes (por exemplo, Leste dos EUA, Oeste de EUA, Europa, Ásia). Caso contrário, os dados do usuário serão distribuídos por várias bordas do AAM.

### media.resume

Se o aplicativo determinar que uma sessão foi encerrada e retomada posteriormente (por exemplo, o usuário saiu do vídeo, mas eventualmente voltou e o reprodutor retomou o vídeo do indicador de reprodução em que parou), você poderá enviar um parâmetro booleano **media.resume** opcional no recipiente de parâmetros da chamada `sessionStart`.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
