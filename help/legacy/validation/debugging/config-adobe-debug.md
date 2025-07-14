---
title: Configurar o Adobe Debug
description: Saiba como configurar o Adobe Debug, que você pode usar para solucionar problemas de implementações do Media SDK.
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
exl-id: 48ad3f23-f36d-44f3-b8d9-b0b3a2ee06bc
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 97%

---

# Configurar o Adobe Debug{#configure-adobe-debug}

## Acessar o Adobe Debug {#accessing-adobe-debug}

Para acessar o Adobe Debug:

1. Acesse a [Experience Cloud](https://www.marketing.adobe.com/) e crie um novo usuário da Adobe Experience Cloud.

   >[!TIP]
   >
   >Este logon não é o mesmo nome de usuário/senha que você usa para fazer logon no Adobe Analytics.

1. Quando tiver uma conta da Experience Cloud, entre em contato com o representante da Adobe para solicitar acesso ao Adobe Debug.
1. Depois de obter o acesso, acesse [https://debug.adobe.com](https://debug.adobe.com) e use suas credenciais da Experience Cloud para fazer logon.

   ![](assets/adobe-debug-login.png)

   Os navegadores compatíveis para esta ferramenta são:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer versões 9-11

Os navegadores recomendados são as versões mais recentes do Chrome e do Firefox.

## Proxy de depuração {#debug-proxy}

Baixe e configure o Proxy de depuração:

1. Baixe o aplicativo Proxy de depuração em [Downloads de aplicativos](https://debug.adobe.com/#/downloads).

   Os sistemas operacionais compatíveis são:
   * OS X 10.7 de 64 bits ou superior
   * Windows 7.1 de 64 bits ou superior

   ![](assets/debug-proxy-app.png)

1. O servidor Proxy de Depuração será executado na sua máquina local na porta 33284 e será definido como proxy do sistema.

   Talvez seja necessário ajustar a configuração do navegador com base no SO e no navegador.

## Baixe e instale o certificado SSL no desktop ou nos aplicativos {#download-and-install-sSL-desktop}

Na primeira vez que você executar a Depuração da Adobe, um certificado SSL exclusivo será gerado. Se você suportar tráfego HTTPS em computadores e/ou aplicativos, será necessário baixar e instalar nosso certificado SSL.

Baixe e instale o certificado SSL:

1. Depois de instalar e iniciar o Adobe Debug, acesse [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) e baixe a certificação.
1. Importe o certificado

   **Mac OS**
   1. Dê duplo clique no certificado CA raiz para abri-lo no Keychain Access.
   1. O certificado CA raiz é exibido no logon.
   1. Mova (arraste) o certificado CA raiz para o Sistema.
   1. Você deve copiar o certificado para o Sistema para garantir que ele seja confiável para todos os usuários e processos do sistema local.
   1. Abra o certificado CA raiz, expanda Confiança, selecione Sempre confiar e salve as alterações.

   **Windows**
   1. Conclua um dos seguintes procedimentos:

      * [Adicionar certificados à loja de Autoridades de Certificação Raiz Confiáveis para um computador local](https://technet.microsoft.com/pt-br/library/cc754841.aspx#BKMK_addlocal)

   1. Para o Firefox, conclua o procedimento em [Instalar o certificado raiz no Mozilla Firefox](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox).

      Você pode precisar sair e reabrir o Firefox para visualizar a alteração.

   **Dispositivos iOS**
   1. Defina seu dispositivo iOS para usar o Adobe Debug como proxy HTTP clicando em **[!UICONTROL Configurações do aplicativo]** **>** **[!UICONTROL Configurações Wi-Fi]**.

   1. No Safari, acesse [Debug](https://proxy.debug.adobe.com/ssl).

      O Safari solicitará que você instale o certificado SSL.

## Instale o Certificado SSL para o seu dispositivo móvel {#install-sSL-for-mobile-device}

Se você não tiver as chamadas HTTPS no Adobe Debug, deverá instalar o Certificado SSL para o Adobe Debug no dispositivo móvel.

### iOS

Para instalar o certificado SSL em um dispositivo iOS:

1. No laptop, ative o Proxy de depuração e vá para o [Adobe Debug](https://debug.adobe.com).
1. Complete as seguintes etapas no dispositivo iOS:
   1. Ative o modo avião do dispositivo.
   1. Selecione o mesmo sinal Wi-Fi usado pelo laptop.
   1. No laptop, defina manualmente o IP e a porta mostrados no aplicativo Debug Proxy.
   1. Abra uma janela do navegador Apple Safari.
   1. Acesse [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl).
   1. Baixe e instale o certificado SSL.

1. No laptop, inicie a sessão de Depuração da Adobe.
1. Inicie o teste no dispositivo iOS.

### Android

Para instalar o certificado SSL em um dispositivo Android:

1. No laptop, ative o Proxy de depuração e vá para o [Adobe Debug](https://debug.adobe.com).
1. Complete as seguintes etapas no dispositivo Android:
   1. Ative o modo avião do dispositivo.
   1. Selecione o mesmo sinal Wi-Fi usado pelo laptop.
   1. No laptop, defina manualmente o IP e a porta mostrados no aplicativo Debug Proxy.
   1. Abra uma janela do navegador.
   1. Acesse [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl).
   1. Baixe e instale o certificado SSL.

1. No laptop, inicie a sessão de Depuração da Adobe.
1. Inicie o teste no dispositivo Android.
