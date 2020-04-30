---
title: Configurar iOS
description: Configuração do aplicativo SDK do Media para implementação no iOS.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Configurar iOS {#set-up-ios}

## Pré-requisitos

* **Obter parâmetros de configuração válidos para o SDK do Media** Esses parâmetros podem ser obtidos de um representante da Adobe após a configuração da sua conta do Analytics.
* **Implementar o ADBMobile para iOS no aplicativo**
Para obter mais informações sobre a documentação do SDK do Adobe Mobile, consulte [SDK do iOS 4.x para Soluções da Experience Cloud.](https://docs.adobe.com/content/help/pt-BR/mobile-services/ios/overview.html)

   >[!IMPORTANT]
   >
   >A partir do iOS 9, a Apple introduziu um recurso chamado App Transport Security (ATS). Esse recurso tem como objetivo melhorar a segurança da rede, garantindo que seus aplicativos usem somente protocolos e cifras padrão do setor. Esse recurso é ativado por padrão, mas você tem opções de configuração que fornecem opções para trabalhar com ATS. Para obter detalhes sobre ATS, consulte [App Transport Security.](https://docs.adobe.com/content/help/en/mobile-services/ios/config-ios/app-transport-security.html)

* **Forneça os seguintes recursos no player de mídia:**

   * _Uma API para assinar eventos do player_ - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * _Uma API que fornece informações sobre o player_ - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

## Implementação do SDK

1. Adicione a biblioteca [baixada](/help/sdk-implement/download-sdks.md#download-2x-sdks) do SDK do Media ao projeto.

   1. Verifique se os componentes de software a seguir existem no diretório `libs`:

      * `ADBMediaHeartbeat.h`: o arquivo do cabeçalho Objective-C usado para APIs de rastreamento de heartbeat no iOS.
      * `ADBMediaHeartbeatConfig.h`: o arquivo do cabeçalho Objective-C usado na configuração do SDK.
      * `MediaSDK.a`: um binário multiarquitetura habilitado para código de bits que contém as compilações de biblioteca para dispositivos iOS (armv7, armv7s, arm64) e simuladores (i386 e x86_64).

         Esse binário deve ser vinculado quando o destino for um aplicativo iOS.

      * `MediaSDK_TV.a`: um binário multiarquitetura habilitado para código de bits, que apresente as compilações de biblioteca para novos dispositivos Apple TV (arm64) e simuladores (x86_64).

         Esse binário deve ser vinculado quando o destino for pretendido para um aplicativo da Apple TV (tvOS).
   1. Adicione a biblioteca ao projeto:

      1. Abra o Xcode IDE e o seu aplicativo.
      1. In **[!UICONTROL Project Navigator]**, drag the `libs` directory and drop it under your project.

      1. Certifique-se de que a caixa de **[!UICONTROL Copy Items if Needed]** seleção esteja selecionada, que **[!UICONTROL Create Groups]** esteja selecionada e que nenhuma das caixas de seleção em **[!UICONTROL Add to Target]** esteja selecionada.

         ![](assets/choose-options_ios.png)

      1. Clique em **[!UICONTROL Finish]**.
      1. In **[!UICONTROL Project Navigator]**, select your app and select your targets.
      1. Link the required frameworks and libraries in the **[!UICONTROL Linked Frameworks]** and **[!UICONTROL Libraries]** section on the **[!UICONTROL General]** tab.

         **Destinos de aplicativos iOS:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**
         **Públicos da Apple TV (tvOS):**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. Verifique se o aplicativo foi criado sem erros.




1. Importe a biblioteca.

   ```
   #import "ADBMediaHeartbeat.h" 
   #import "ADBMediaHeartbeatConfig.h" 
   ```

1. Crie uma instância `ADBMediaHeartbeatConfig`.

   Essa seção ajuda você a entender os parâmetros de configuração do `MediaHeartbeat` e definir corretamente os valores de configuração na sua instância `MediaHeartbeat`, de modo a permitir um rastreamento preciso.

   Aqui está uma amostra de inicialização `ADBMediaHeartbeatConfig`:

   ```
   // Media Heartbeat Initialization 
   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
   config.trackingServer = <SAMPLE_HEARTBEAT_TRACKING_SERVER>; 
   config.channel        = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion     = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp            = <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName     = <SAMPLE_PLAYER_NAME>; 
   config.ssl            = <YES/NO>; 
   config.debugLogging   = <YES/NO>; 
   ```

1. Implemente o protocolo `ADBMediaHeartbeatDelegate`.

   ```
   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 
   
   @end 
   
   @implementation VideoAnalyticsProvider 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
   // with the current playback QoS values. 
   - (ADBMediaObject *)getQoSObject { 
       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
                                 startupTime:<startuptime>   
                                 fps:<fps>  
                                 droppedFrames:<droppedFrames>]; 
   } 
   
   // Return the current video player playhead position. 
   // Replace <currentPlaybackTime> with the video player current playback time 
   - (NSTimeInterval)getCurrentPlaybackTime { 
       return <currentPlaybackTime>; 
   } 
   
   @end
   ```

1. Use `ADBMediaHeartBeatConfig` e `ADBMediaHeartBeatDelegate` para criar a instância `ADBMediaHeartbeat`.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Certifique-se de que a instância `ADBMediaHeartbeat` possa ser acessada e *não seja desalocada até o final da sessão*. Essa instância será usada para todos os eventos de rastreamento a seguir.

## Migração da versão 1.x para 2.x do iOS {#migrate-to-two-x}

Na versão 2.x, todos os métodos públicos foram consolidados na classe `ADBMediaHeartbeat` para facilitar o trabalho dos desenvolvedores. Todas as configurações foram consolidadas na classe `ADBMediaHeartbeatConfig`.

Para obter mais informações sobre a migração de 1.x para 2.x, consulte [Migração do VHL 1.x para 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Configuração de um aplicativo nativo para tvOS

Com o lançamento da nova Apple TV, agora é possível criar aplicativos para execução no ambiente tvOS nativo. Você pode criar um aplicativo puramente nativo, usando qualquer uma das várias estruturas disponíveis no iOS, ou criar seu aplicativo usando modelos XML e JavaScript. A partir da versão 2.0 do SDK do Media, o suporte para tvOS está disponível. Para mais informações sobre tvOS, consulte o [Site do desenvolvedor do tvOS.](https://developer.apple.com/tvos/)

Execute as seguintes etapas no projeto Xcode. Este guia foi escrito supondo que seu projeto tem um público-alvo que é um aplicativo da Apple TV direcionado ao tvOS:

1. Arraste o arquivo de biblioteca `VideoHeartbeat_TV.a` para a pasta `lib` do seu projeto.

1. Na guia **[!UICONTROL Build Phases]** do público alvo do aplicativo tvOS, expanda a seção **[!UICONTROL Link Binary with Libraries]** e adicione as seguintes bibliotecas:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

