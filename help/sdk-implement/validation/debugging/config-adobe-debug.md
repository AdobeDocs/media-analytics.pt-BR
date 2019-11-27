---
title: Configurar o Adobe Debug
description: Este tópico descreve como configurar o Adobe Debug, que você pode usar para solucionar problemas de implementações do SDK do Media.
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Configurar o Adobe Debug {#configure-adobe-debug}

## Acessar o Adobe Debug {#accessing-adobe-debug}

Para acessar o Adobe Debug:

1. Acesse a [Experience Cloud](https://www.marketing.adobe.com) e crie um novo usuário da Adobe Experience Cloud.

   >[!TIP]
   >
   >Este logon não é o mesmo nome de usuário/senha que você usa para fazer logon no Adobe Analytics.

1. Quando tiver uma conta da Experience Cloud, entre em contato com o representante da Adobe para solicitar acesso ao Adobe Debug.
1. Depois de obter o acesso, acesse [https://debug.adobe.com](https://debug.adobe.com) e use suas credenciais da Experience Cloud para fazer logon.

   ![](assets/adobe-debug-login.png)

   Os navegadores compatíveis com esta ferramenta são:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer versões 9 a 11

Os navegadores recomendados são as versões mais recentes do Chrome e do Firefox.

## Proxy de depuração {#debug-proxy}

Baixe e configure o Proxy de depuração:

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

1. Depois de instalar e iniciar o Adobe Debug, acesse [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) e baixe a certificação.
1. Importe o certificado

   **Mac OS**
   1. Clique duas vezes no certificado da autoridade de certificação de raiz para abri-lo no Keychain Access.
   1. O certificado da autoridade de certificação de raiz é exibido no logon.
   1. Mova (arraste) o certificado da autoridade de certificação de raiz para o sistema.
   1. Você deve copiar o certificado para o sistema para garantir sua confiança por todos os usuários e processos do sistema local.
   1. Abra o certificado da autoridade de certificação de raiz, expanda Confiança, selecione Sempre confiar e salve as alterações.
   **Windows**
   1. Realize um dos seguintes procedimentos:

      * [Adicionar certificados ao repositório de Autoridades de certificação de raiz confiáveis a um computador local](https://technet.microsoft.com/pt-br/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1. Para o Firefox, conclua o procedimento em [Instalar o certificado raiz no Mozilla Firefox.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)
    
    Talvez seja necessário sair e reabrir o Firefox para ver a alteração.
    
    **Dispositivos iOS**
    1. Defina seu dispositivo iOS para usar o Adobe Debug como proxy HTTP clicando em **[!UICONTROL Configurações do aplicativo]** **&gt;** **[!UICONTROL Configurações do Wi-Fi]**.
    
    1. No Safari, acesse [Debug.](https://proxy.debug.adobe.com/ssl)
    
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
   1. Acesse [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
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
   1. Acesse [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Baixe e instale o certificado SSL.

1. No laptop, inicie a sessão do Adobe Debug.
1. Inicie o teste no seu dispositivo Android.

