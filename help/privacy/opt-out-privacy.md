---
title: Explicação sobre a opção de rejeição e privacidade
description: Aprenda a gerenciar a opção de aceitação, rejeição e privacidade.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c00c9850d5ea924cef6b4842ecb770df1e78eb21
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 94%

---

# Opção de rejeição e privacidade {#opt-out-and-privacy}

## Opção de rejeição/aceitação {#opt-out-opt-in}

Você pode decidir se uma atividade de rastreamento é permitida em um determinado dispositivo:

* **Aplicativos para dispositivos móveis -** As extensões de mídia respeitam as configurações de privacidade na coleção de dados. Para recusar o rastreamento, você precisa configurar a privacidade como [Recusar tags](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/#create-a-mobile-property) ou [Atualizar o status de privacidade no SDK móvel](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#getprivacystatus).
* **Aplicativos do JavaScript/navegador -** A biblioteca do VA respeita as configurações de recusa e privacidade da biblioteca do `VisitorAPI`. Para excluir o rastreamento do, você precisa fazer a exclusão do serviço Visitor API. Para obter mais informações sobre recusa e privacidade, consulte [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR).
* **Os aplicativos OTT (Chromecast, Roku) -** Os SDKs de OTT fornecem APIs preparadas para o Regulamento Geral sobre a Proteção de Dados (GDPR), que permitem definir sinalizadores de status `opt` para a coleta e a transmissão de dados e para recuperar as identidades armazenadas localmente.

  >[!NOTE]
  >
  >As chamadas de rastreamento de heartbeat de mídia também estarão desativadas se o status de privacidade estiver definido como recusar.

  Você pode decidir se os dados do Analytics são enviados ou não em um determinado dispositivo usando as seguintes configurações:

   * A configuração `privacyDefault` no arquivo de configuração `ADBMobile.json` Isso controla a configuração inicial e é mantida até a alteração no código.

   * O método `ADBMobile().setPrivacyStatus()`.

      * **Rejeitar:**

         * **Chromecast:**

           ```
           ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
           ```

         * **Roku:**

           ```
           ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
           ```

        >[!IMPORTANT]
        >
        >Quando um usuário recusa o rastreamento, todos os dados e IDs persistentes do dispositivo são removidos até que o usuário volte a aceitar o rastreamento.

      * **Ativar novamente:**

         * **Chromecast:**

           ```
           ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
           ```

         * **Roku:**

           ```
           ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
           ```

      * **Retorna a configuração atual:**

         * **Chromecast:**

           ```
           ADBMobile.config.getPrivacyStatus()
           ```

         * **Roku:**

           ```
           ADBMobile().getPrivacyStatus()
           ```

  Depois de alterar a configuração de privacidade usando `setPrivacyStatus`, a alteração torna-se permanente até ser alterada novamente usando este método ou ao desinstalar e instalar o aplicativo.

## Recuperar identificadores armazenados (aplicativos OTT) {#retrieving-stored-identifiers-ott-apps}

Essas informações ajudam a recuperar identidades de usuário armazenadas localmente do aplicativo Roku.

>[!IMPORTANT]
>
>O método para recuperar todos os identificadores obtém todas as identidades de usuário conhecidas e persistidas pelo SDK. Você deve chamar esse método **antes** de um usuário recusar.

As identidades armazenadas localmente são retornadas em uma sequência JSON, que pode conter:

* Contexto da empresa - IDs de organização IMS
* IDs de usuário
* Experience Cloud ID (MCID)
* IDs de fonte de dados (DPID, DPUUID)
* IDs do Analytics (AVID, AID, VID e RSIDs associados)
* ID do Audience Manager (UUID)

Por exemplo:

* **Chromecast:**

  ```
  ADBMobile.config.getAllIdentifiersAsync(callback)
  ```

* **Roku:**

  ```
  vids = ADBMobile().getAllIdentifiers()
  ```
