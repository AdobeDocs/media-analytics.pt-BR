---
title: O que é a ativação do Adobe Audience Manager?
description: Saiba como vincular ações do aplicativo aos dados de rastreamento de mídia sem precisar de regras de processamento adicionais e variáveis personalizadas.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oInE3GwgI1k5-UbqMUm9yvjXfIF0SsRXPrnUWmWT9Ww
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 100%

---

# Ativação do Audience Manager{#audience-manager-enablement}

O Adobe Audience Manager (AAM), uma plataforma de gerenciamento de dados (DMP), ajuda a reunir os ativos de dados do seu público, facilitando a coleta de informações comercialmente relevantes sobre os visitantes do site, a criação de segmentos comercializáveis e a veiculação de conteúdo e publicidade direcionada ao público certo.

Com o AAM, você não está vinculado a um vendedor de dados, troca ou plataforma do lado da demanda. Além disso, o AAM é completamente agnóstico quando se trata dos ativos de dados de seus parceiros. Com acesso a várias fontes de dados, o AAM oferece aos publicadores digitais a capacidade de usar uma grande variedade de dados de terceiros. Para saber mais sobre o AAM, consulte a documentação do AAM [Documentação do produto Audience Manager](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.html).

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
