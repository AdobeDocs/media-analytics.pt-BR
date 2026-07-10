---
title: Configurações de recusa e privacidade
description: Aprenda a gerenciar a opção de aceitação, rejeição e privacidade.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 8b9e7582923a61bd2a43049a02ce36727a677e17
workflow-type: tm+mt
source-wordcount: 798
ht-degree: 3%

---

# Configurações de recusa e privacidade

Quando um usuário recusa o rastreamento, a biblioteca de mídia de transmissão interrompe imediatamente todas as atividades de coleta de dados. Nenhuma chamada de início de sessão, nenhum ping de heartbeat e nenhum dado de rastreamento de eventos é enviado aos servidores de coleta de dados da Adobe para esse usuário.

## Opção de rejeição/aceitação

Os controles de recusa operam por dispositivo ou navegador. O respeito pelo consentimento do usuário é responsabilidade da organização de implementação. Para obter uma visão geral das práticas de privacidade da Adobe, consulte o [Centro de Privacidade da Adobe](https://www.adobe.com/br/privacy.html).

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

O Web SDK respeita as preferências de consentimento definidas usando o comando `setConsent`. Quando o consentimento é definido como `"out"`, o Web SDK interrompe o encaminhamento de todos os eventos, incluindo chamadas de rastreamento de streaming de mídia, para a Edge Network. O estado de consentimento persiste no armazenamento do navegador entre as sessões.

Antes de implementar a opção de recusa, verifique se o Web SDK está configurado com o componente de Mídia de transmissão. Para obter mais informações, consulte [Configurar Web SDK](../implementation/edge/web-sdk.md).

Definir o consentimento para recusa usando o padrão de consentimento do Adobe 2.0:

```javascript
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: { val: "n" }
    }
  }]
});
```

Valores de consentimento:

* `"y"`: Aceitação (coleta de dados permitida)
* `"n"`: Recusa (coleta de dados suprimida)
* `"p"`: Pendente (aguardando decisão do usuário; nenhum dado coletado até ser resolvido)

Para restaurar o rastreamento, chame `setConsent` novamente com `"y"` como o valor `collect.val`.

Consulte o [comando setConsent](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/commands/setconsent) na documentação do Web SDK para outros formatos, incluindo o IAB TCF 2.0.

>[!TAB iOS]

O Adobe Experience Platform Mobile SDK respeita o status de privacidade definido usando `MobileCore.setPrivacyStatus()`. Definir o status como `.optedOut` suprime toda a coleta de dados em todas as extensões do AEP, incluindo Mídia de Streaming. O status persiste entre sessões de aplicativo.

```swift
MobileCore.setPrivacyStatus(.optedOut)
```

Para restaurar o rastreamento, defina o status de privacidade novamente como `.optedIn`:

```swift
MobileCore.setPrivacyStatus(.optedIn)
```

Para obter mais informações, consulte [Privacidade e GDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus) na documentação do AEP Mobile SDK.

>[!TAB Android]

O Adobe Experience Platform Mobile SDK respeita o status de privacidade definido usando `MobileCore.setPrivacyStatus()`. Definir o status como `MobilePrivacyStatus.OPT_OUT` suprime toda a coleta de dados em todas as extensões do AEP, incluindo Mídia de Streaming. O status persiste entre sessões de aplicativo.

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT)
```

Para restaurar o rastreamento, defina o status de privacidade novamente como `MobilePrivacyStatus.OPT_IN`:

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_IN)
```

Para obter mais informações, consulte [Privacidade e GDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus) na documentação do AEP Mobile SDK.

>[!TAB Roku Edge]

O SDK do Roku Edge usa `setConsent()` com o padrão de consentimento do Adobe 2.0. A configuração de `collect.val` a `"n"` interrompe imediatamente toda a coleta de dados, incluindo os eventos de streaming de mídia.

Valores de consentimento:

* `"y"`: Aceitação (coleta de dados permitida)
* `"n"`: Recusa (coleta de dados suprimida)
* `"p"`: Pendente (aguardando decisão do usuário; nenhum dado coletado até ser resolvido)

```brightscript
currentDate = CreateObject("roDateTime")
timestampInISO8601 = currentDate.ToISOString("milliseconds")

collectConsentNo = {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "metadata": { "time": timestampInISO8601 },
      "collect": { "val": "n" }
    }
  }]
}

m.aepSdk.setConsent(collectConsentNo)
```

Para restaurar o rastreamento, defina `collect.val` como `"y"` e chame `setConsent()` novamente.

Você também pode definir um valor de consentimento padrão na inicialização do SDK usando `updateConfiguration()` com a chave `ADB_CONSTANTS.CONFIGURATION.CONSENT_DEFAULT`. Para obter mais informações, consulte a [documentação do Roku Edge SDK](https://github.com/adobe/aepsdk-roku).

>[!TAB API do Media Edge]

A API do Media Edge é uma implementação do lado do servidor. Nenhuma camada do SDK impõe o consentimento automaticamente — seu aplicativo deve verificar o status de consentimento do usuário antes de fazer qualquer chamada de API e suprimir solicitações de usuários que se excluíram.

Para recusa total, não PUBLIQUE no ponto de extremidade `/va/v2/sessions` (ou em qualquer ponto de extremidade de evento subsequente) para usuários que recusaram:

```javascript
// Check consent status before initiating a media session
if (userHasOptedOut) {
  // Do not call the Media Edge API
  return;
}

// Only call the API for users who have not opted out
fetch("https://edge.adobedc.net/va/v2/sessions", {
  method: "POST",
  body: JSON.stringify(sessionStartPayload)
});
```

Para obter mais informações, consulte a [API do Media Edge](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/).

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

A biblioteca Media SDK JS 3.x adia para o estado de não participação da API do visitante da Adobe (serviço de identidade). Quando um usuário recusa o uso da API de visitante, o Media SDK suprime automaticamente todas as chamadas de rastreamento.

```javascript
var visitor = Visitor.getInstance("YOUR_ORG_ID@AdobeOrg");
visitor.setOptOut(true);
```

Substitua `YOUR_ORG_ID@AdobeOrg` pela ID da organização da Adobe Admin Console.

Para restaurar o rastreamento, passe `false` para `setOptOut()`.

Para obter mais informações, consulte [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR).

>[!TAB Chromecast]

O Chromecast Media SDK 3.x respeita o status de privacidade definido usando `ADBMobile.config.setPrivacyStatus()`. Definir o status como `PRIVACY_STATUS_OPT_OUT` suprime toda a coleta de dados.

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT);
```

Para restaurar o rastreamento, defina o status novamente como Opted in:

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN);
```

Você também pode definir o status de privacidade padrão na inicialização do SDK no objeto `ADBMobileConfig`:

```javascript
var ADBMobileConfig = {
  "analytics": {
    "privacyDefault": "optedout"
  }
};
```

>[!TAB Roku 2.x]

O Roku 2.x SDK respeita o status de privacidade definido usando `setPrivacyStatus`. Definir o status como `PRIVACY_STATUS_OPT_OUT` suprime toda a coleta de dados.

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_OUT)
```

Para restaurar o rastreamento, defina o status novamente como Opted in:

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_IN)
```

Você também pode definir o status de privacidade padrão na inicialização do SDK no arquivo `ADBMobileConfig.json`:

```json
"analytics": {
  "privacyDefault": "optedout"
}
```

>[!TAB API da coleção de mídia]

A API da coleção de mídia é uma implementação do lado do servidor. Seu aplicativo deve verificar o status de consentimento do usuário antes de fazer chamadas de API e suprimir solicitações de usuários que recusaram a adesão.

Para recusa completa, não publique no endpoint de sessões para usuários que recusaram.

Para recusas parciais em CCPA, inclua sinalizadores de recusa no objeto `params` de sua solicitação `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "analytics.optOutServerSideForwarding": true,
    "analytics.optOutShare": true
  }
}
```

* `analytics.optOutServerSideForwarding`: Defina como `true` para recusar o compartilhamento de dados entre a Adobe Analytics e outras soluções da Experience Cloud (como o Audience Manager).
* `analytics.optOutShare`: Defina como `true` para recusar o compartilhamento de dados federados com outros clientes do Adobe Analytics.

Para obter uma lista completa dos parâmetros disponíveis, consulte a [Referência de parâmetros da solicitação da API Media Collection](../implementation/media-collection-api/mc-api-ref/mc-api-req-params.md).

>[!ENDTABS]
