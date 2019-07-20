---
seo-title: Configurar iOS
title: Configurar iOS
uuid: a 1 c 6 be 79-a 6 dc -47 b 6-93 b 3-ac 7 b 42 f 1 f 3 eb
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# Configurar iOS{#set-up-ios}

## Pré-requisitos

* **Obter parâmetros de configuração válidos para o SDK
de mídia** Esses parâmetros podem ser obtidos a partir de um representante da Adobe depois que você configurar sua conta de análise.
* **Implementação do adbmobile para iOS em seu aplicativo**
Para obter mais informações sobre a documentação do SDK do Adobe Mobile, consulte [iOS SDK 4. x para Soluções da Experience Cloud.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/)

   >[!IMPORTANT]
   >
   >A partir do iOS 9, a Apple apresentou um recurso chamado App Transport Security (ATS). Este recurso visa melhorar a segurança da rede, garantindo que seus aplicativos usem somente protocolos padrão do setor e cifras. Esse recurso é ativado por padrão, mas você tem opções de configuração que permitem trabalhar com ATS. For details on ATS, see [App Transport Security.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html)

* **Forneça os seguintes recursos no reprodutor de mídia:**

   * _Uma API para assinar os eventos do reprodutor_ - O SDK do Media exige a chamada de um conjunto de APIs simples quando ocorrerem eventos no reprodutor.
   * _Uma API que fornece informações sobre o reprodutor_ - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

## Implementação do SDK

1. Adicione a biblioteca [baixada](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) do SDK do Media ao projeto.

   1. Verifique se os componentes de software a seguir existem no diretório `libs`:

      * `ADBMediaHeartbeat.h`: o arquivo do cabeçalho Objective-C usado para APIs de rastreamento de heartbeat no iOS.
      * `ADBMediaHeartbeatConfig.h`: o arquivo do cabeçalho Objective-C usado na configuração do SDK.
      * `MediaSDK.a`: um binário multiarquitetura habilitado para código de bits que contém as compilações de biblioteca para dispositivos iOS (armv7, armv7s, arm64) e simuladores (i386 e x86_64).

         Esse binário deve ser vinculado quando o destino for um aplicativo iOS.

      * `MediaSDK_TV.a`: um binário multiarquitetura habilitado para código de bits, que apresente as compilações de biblioteca para novos dispositivos Apple TV (arm64) e simuladores (x86_64).

         Esse binário deve ser vinculado quando o destino for um aplicativo da Apple TV (tvOS).
   1. Adicionar a biblioteca ao projeto:

      1. Abra o Xcode IDE e o seu aplicativo.
      1. No **[!UICONTROL Navegador do projeto]**, arraste o diretório `libs` e solte-o no seu projeto.

      1. Certifique-se de que as caixas de seleção **[!UICONTROL Copiar itens se necessário]** e **[!UICONTROL Criar grupos]estejam marcadas e que nenhuma das caixas de seleção em** Adicionar ao destino] estejam selecionadas.**[!UICONTROL **

         ![](assets/choose-options_ios.png)

      1. Clique em **[!UICONTROL Concluir]**.
      1. In **[!UICONTROL Project Navigator]**, select your app and select your targets.
      1. Vincule as estruturas e bibliotecas necessárias na seção **[!UICONTROL Estruturas vinculadas]** e **[!UICONTROL Bibliotecas]** na guia **[!UICONTROL Geral]**.

         **Destinos de aplicativos iOS:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**
         **Destinos da Apple TV (tvOS)**:

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

1. Create a `ADBMediaHeartbeatConfig` instance.

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

1. Implement the `ADBMediaHeartbeatDelegate` protocol.

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

1. Use the `ADBMediaHeartBeatConfig` and `ADBMediaHeartBeatDelegate` to create the `ADBMediaHeartbeat` instance.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `ADBMediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. Essa instância será usada para todos os eventos de rastreamento a seguir.

## Migração da versão 1.x para 2.x do iOS {#migrate-to-two-x}

Na versão 2.x, todos os métodos públicos foram consolidados na classe `ADBMediaHeartbeat` para facilitar o trabalho dos desenvolvedores. Todas as configurações foram consolidadas na classe `ADBMediaHeartbeatConfig`.

Para obter mais informações sobre a migração de 1.x para 2.x, consulte [Migração do VHL 1.x para 2.x.](../../sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Configuração de um aplicativo nativo para tvOS

Com o lançamento da nova Apple TV, é possível criar aplicativos compatíveis com um ambiente tvOS nativo. Você pode criar um aplicativo completamente nativo com as várias estruturas disponíveis no iOS, ou criar seu próprio aplicativo usando modelos XML e JavaScript. A partir da versão 2.0 do SDK do Media, o suporte para tvOS está disponível. Para mais informações sobre tvOS, consulte o [Site do desenvolvedor do tvOS.](https://developer.apple.com/tvos/documentation/)

Execute as seguintes etapas no projeto Xcode. Este guia foi escrito supondo que seu projeto tenha um direcionamento o aplicativo Apple TV com segmentação tvOS:

1. Drag the `VideoHeartbeat_TV.a` library file into your project’s `lib` folder.

1. Na guia **[!UICONTROL Criar fases]** do destino do seu aplicativo tvOS, expanda a seção **[!UICONTROL Link binário com bibliotecas]** e adicione as seguintes bibliotecas:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

