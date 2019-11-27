---
title: Opção de rejeição e privacidade
description: Como lidar com aceitação, recusa e privacidade.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Opção de rejeição e privacidade {#opt-out-and-privacy}

## Opção de rejeição/aceitação {#opt-out-opt-in}

Você pode decidir se uma atividade de rastreamento é permitida em um determinado dispositivo:

* **Aplicativos móveis -** A biblioteca do VA respeita as configurações de recusa e privacidade da biblioteca do `AdobeMobile`. Para recusar o rastreamento, você precisa usar a biblioteca do `AdobeMobile`. Para obter mais informações sobre as configurações de recusa e privacidade da `AdobeMobile`, consulte [Configurações de recusa e privacidade](https://docs.adobe.com/content/help/pt-BR/mobile-services/android/gdpr-privacy-android/privacy.html).
* **Aplicativos do JavaScript/navegador -** A biblioteca do VA respeita as configurações de recusa e privacidade da biblioteca do `VisitorAPI`. Para excluir o rastreamento do, você precisa fazer a exclusão do serviço Visitor API. Para obter mais informações sobre recusa e privacidade, consulte [Serviço de Identidade da Adobe Experience Platform.](https://marketing.adobe.com/resources/help/pt_BR/mcvid/)
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

      * **Aceitar novamente:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **Retornar a configuração atual:**

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
>O método para recuperar todos os identificadores obtém todas as identidades de usuário conhecidas e persistidas pelo SDK. Você deve chamar esse método **antes** que usuário cancele a adesão.

As identidades armazenadas localmente são retornadas em uma sequência de caracteres JSON, que pode conter:

* Contexto da empresa - IDs de org IMS
* IDs de usuário
* Experience Cloud ID (MCID)
* IDs da fonte de dados (DPID, DPUUID)
* Analytics IDs (AVID, AID, VID e RSIDs associados)
* Audience Manager ID (UUID)

Por exemplo:

* **Chromecast:**

   ```
   ADBMobile.config.getAllIdentifiersAsync(callback)
   ```

* **Roku:**

   ```
   vids = ADBMobile().getAllIdentifiers()
   ```

