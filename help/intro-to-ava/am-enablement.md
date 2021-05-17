---
title: O que é a ativação do Adobe Audience Manager?
description: Saiba como vincular ações do aplicativo aos dados de rastreamento de mídia sem precisar de regras de processamento adicionais e variáveis personalizadas.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
source-git-commit: e781af84f23400aa7c899b686f0e9fee2c19d660
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 100%

---

# Ativação do Audience Manager {#audience-manager-enablement}

O Adobe Audience Manager (AAM), uma plataforma de gerenciamento de dados (DMP), ajuda a reunir os ativos de dados do seu público, facilitando a coleta de informações comercialmente relevantes sobre os visitantes do site, a criação de segmentos comercializáveis e a veiculação de conteúdo e publicidade direcionada ao público certo.

Com o AAM, você não está vinculado a um vendedor de dados, troca ou plataforma do lado da demanda. Além disso, o AAM é completamente agnóstico quando se trata dos ativos de dados de seus parceiros. Com acesso a várias fontes de dados, o AAM oferece aos publicadores digitais a capacidade de usar uma grande variedade de dados de terceiros e nosso Data Co-op privado. Para saber mais sobre o AAM, consulte a documentação do AAM [Documentação do produto Audience Manager.](https://docs.adobe.com/content/help/pt-BR/audience-manager/user-guide/aam-home.html)

**Transferência dados do VA para o AAM -** Para conteúdo em vídeo e anúncios em vídeo, as métricas e os metadados coletados usando variáveis de solução (reservadas) podem ser automaticamente enviados para o AAM. A transferência de dados está disponível em todas as plataformas, como desktop, dispositivos móveis e OTT. Para habilitar essa transferência de dados do lado do servidor, é necessário entrar em contato com o Atendimento ao cliente da Adobe e solicitar que esse feed seja habilitado.

>[!IMPORTANT]
>
>Para garantir a transferência perfeita de dados para o AAM, você deve ter as versões mais recentes das bibliotecas do SDK do Media.

Os dados federados oferecem suporte total ao compartilhamento de dados no AAM. Entre em contato com a equipe da Adobe para obter a confirmação das configurações de Dados federados.

## Métodos OTT/AAM {#ott-aam-methods}

Você pode usar esses métodos para enviar sinais e recuperar segmentos de visitantes do Audience Manager:

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   Retorna o perfil do visitante obtido recentemente. Retorna um objeto vazio se nenhum sinal tiver sido enviado.

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   Retorna o perfil do visitante obtido recentemente. Retorna um objeto vazio se nenhum sinal tiver sido enviado.

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   Retorna a DPUUID atual.

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   Define a DPID e a DPUUID. Se DPID e DPUUID estiverem definidas, elas serão enviadas com cada sinal.

   ```js
   ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   Envia ao gerenciamento de público-alvo um sinal com características.

   ```js
   ADBMobile.audienceManager.submitSignal({"sampleTrait":"sampleValue"});
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   Retorna o perfil do visitante obtido recentemente. Retorna um objeto vazio se nenhum sinal tiver sido enviado.

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   Retorna o perfil do visitante obtido recentemente. Retorna um objeto vazio se nenhum sinal tiver sido enviado.

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   Retorna a DPUUID atual.

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   Define a DPID e a DPUUID. Se DPID e DPUUID estiverem definidas, elas serão enviadas com cada sinal.

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   Envia ao gerenciamento de público-alvo um sinal com características.

   ```js
   traitData = {}
   traitData["sampleTrait"] = "sampleValue"
   ADBMobile().audienceSubmitSignal(traitData)
   ```
