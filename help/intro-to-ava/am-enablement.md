---
title: Ativação do Audience Manager
description: null
uuid: 8a7f9343-ebc3-4087-9d7e-5972640d2455
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Ativação do Audience Manager {#audience-manager-enablement}

O Adobe Audience Manager (AAM), uma plataforma de gerenciamento de dados (DMP), ajuda você a unir seus ativos de dados de público, facilitando a coleta de informações comercialmente relevantes sobre os visitantes, a criação de segmentos comercializáveis e o fornecimento de publicidade e conteúdo direcionados ao público certo.

Com o AAM, você não fica vinculado a uma plataforma de venda, troca ou demanda de dados. Além disso, o AAM é completamente independente quando se trata dos ativos de dados dos seus parceiros. Com acesso a várias fontes de dados, o AAM oferece aos publicadores digitais a capacidade de usar uma grande variedade de dados de terceiros e nosso Data Co-op privado. Para saber mais sobre o AAM, consulte a documentação do AAM [Documentação do produto Audience Manager.](https://docs.adobe.com/content/help/pt-BR/audience-manager/user-guide/aam-home.html)

**Transferência de dados do VA para o AAM -** Tanto para o conteúdo de vídeo quanto para os anúncios de vídeo, as métricas e os metadados coletados usando variáveis de solução (reservadas) podem ser enviados automaticamente para o AAM. A transferência de dados está disponível em todas as plataformas, incluindo desktops, celulares e OTTs. Para habilitar essa transferência de dados no lado do servidor, você precisa entrar em contato com o Atendimento ao cliente da Adobe e solicitar a ativação desse feed.

>[!IMPORTANT]
>
>Para garantir a transferência perfeita de dados para o AAM, você deve ter as versões mais recentes das bibliotecas do SDK do Media.

Os dados federados são completamente compatíveis com o compartilhamento de dados com o AAM. Trabalhe com a sua equipe da Adobe para confirmar as configurações dos dados federados.

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
   ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   Envia ao gerenciamento de público-alvo um sinal com características.

   ```js
   ADBMobile.audienceManager.SubmitSignal();
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
   ADBMobile().audienceSubmitSignal()
   ```

