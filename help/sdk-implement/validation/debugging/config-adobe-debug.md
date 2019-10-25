---
seo-title: Configurar o Adobe Debug
title: Configurar o Adobe Debug
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# Configurar o Adobe Debug{#configure-adobe-debug}

## Acessar o Adobe Debug {#accessing-adobe-debug}

Para acessar o Adobe Debug:

1. Go to [Experience Cloud](https://www.marketing.adobe.com) and create a new Adobe Experience Cloud user.

   >[!TIP]
   >
   >Esse logon não é o mesmo nome de usuário/senha que você usa para fazer logon no Adobe Analytics.

1. Quando tiver uma conta da Experience Cloud, entre em contato com o representante da Adobe para solicitar acesso ao Adobe Debug.
1. After access has been granted, go to [https://debug.adobe.com](https://debug.adobe.com) and use your Experience Cloud credentials to log in.

   ![](assets/adobe-debug-login.png)

   Os navegadores compatíveis com esta ferramenta são:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer versões 9 a 11

Os navegadores recomendados são as versões mais recentes do Chrome e do Firefox.

## Proxy de depuração {#debug-proxy}

Baixe e configure o proxy de depuração:

1. Baixe o aplicativo Proxy de depuração em [Downloads de aplicativos.](https://debug.adobe.com/#/downloads)

   Os sistemas operacionais compatíveis são:
   * OS X 10.7 de 64 bits ou superior
   * Windows 7.1 de 64 bits ou superior
   ![](assets/debug-proxy-app.png)

1. O servidor proxy de depuração será executado na máquina local na porta 33284 e será definido como o proxy do sistema.

   Talvez seja necessário ajustar as configurações do navegador de acordo com o sistema operacional e o navegador.

## Baixe e instale o certificado SSL no desktop ou nos aplicativos {#download-and-install-sSL-desktop}

Um certificado SSL exclusivo será gerado na primeira vez que você executar o Adobe Debug. Se você oferecer suporte ao tráfego HTTPS através do desktop e/ou dos aplicativos, precisará baixar e instalar nosso certificado SSL.

Baixe e instale o certificado SSL:

1. After Adobe Debug has been installed and started, go to [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) and download the certification.
1. Importe o certificado

   **Mac OS**
   1. Clique duas vezes no certificado da autoridade de certificação de raiz para abri-lo no Keychain Access.
   1. O certificado da autoridade de certificação de raiz é exibido no logon.
   1. Mova (arraste) o certificado da autoridade de certificação de raiz para o sistema.
   1. Você deve copiar o certificado para o sistema para garantir sua confiança por todos os usuários e processos do sistema local.
   1. Abra o certificado da autoridade de certificação de raiz, expanda Confiança, selecione Sempre confiar e salve as alterações.
   **Windows**
   1. Realize um dos seguintes procedimentos:

      * [Adicionar certificados ao repositório de Autoridades de certificação de raiz confiáveis a um computador local](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1. Para o Firefox, conclua o procedimento em [Instalação do certificado raiz no Mozilla Firefox].](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)
    
    Talvez seja necessário sair e reabrir o Firefox para ver a alteração.
    
    **Dispositivos iOS**
    1. Set your iOS device to use Adobe Debug as its HTTP proxy by clicking **[!UICONTROL Settings app]** **&gt;** **[!UICONTROL Wifi settings]**.
    
    1. No Safari, vá para [Depuração].](https://proxy.debug.adobe.com/ssl)
    
    O Safari solicitará a instalação do certificado SSL.

## Instale o Certificado SSL para o seu dispositivo móvel {#install-sSL-for-mobile-device}

Se você não tiver as chamadas HTTPS no Adobe Debug, deverá instalar o Certificado SSL para o Adobe Debug no dispositivo móvel.

### iOS

Para instalar o certificado SSL em um dispositivo iOS:

1. No laptop, ative o Proxy de depuração e vá para o [Adobe Debug.](https://debug.adobe.com)
1. Conclua as seguintes etapas no seu dispositivo iOS:
   1. Ligue o dispositivo no modo avião.
   1. Selecione o mesmo sinal Wi-Fi usado pelo seu laptop.
   1. No laptop, defina manualmente o IP e a porta mostrados no aplicativo do Proxy de depuração.
   1. Abra uma janela do navegador Apple Safari.
   1. Go to [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Baixe e instale o certificado SSL.

1. No laptop, inicie a sessão do Adobe Debug.
1. Inicie o teste no seu dispositivo iOS.

### Android

Para instalar o certificado SSL em um dispositivo Android:

1. No laptop, ative o Proxy de depuração e vá para o [Adobe Debug.](https://debug.adobe.com)
1. Conclua as seguintes etapas no seu dispositivo Android:
   1. Defina o dispositivo como Modo avião.
   1. Selecione o mesmo sinal Wi-Fi usado pelo seu laptop.
   1. No laptop, defina manualmente o IP e a porta mostrados no aplicativo do Proxy de depuração.
   1. Abra uma janela do navegador.
   1. Go to [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Baixe e instale o certificado SSL.

1. No laptop, inicie a sessão do Adobe Debug.
1. Inicie o teste no seu dispositivo Android.

