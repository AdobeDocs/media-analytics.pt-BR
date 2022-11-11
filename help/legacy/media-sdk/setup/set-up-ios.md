---
title: Como configurar o SDK de mídia no iOS
description: Siga estas etapas para configurar o aplicativo do SDK de mídia no iOS.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
exl-id: fe7662b5-1700-4bd6-b542-66aa8493459d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 98%

---

# Configurar iOS{#set-up-ios}

Saiba como configurar o Streaming Media Analytics para dispositivos iOS.

>[!IMPORTANT]
>
>Com o fim do suporte para SDKs móveis da versão 4 em 31 de agosto de 2021, a Adobe também encerrará o suporte para o SDK do Media Analytics para iOS e Android.  Para obter mais informações, consulte [Perguntas frequentes sobre o fim do suporte do SDK do Media Analytics](/help/additional-resources/end-of-support-faqs.md).

## Pré-requisitos

* **Obter parâmetros de configuração válidos para o SDK do Media** Esses parâmetros podem ser obtidos de um representante da Adobe após a configuração da sua conta do Analytics.
* **Implementar o ADBMobile para iOS no aplicativo**
Para obter mais informações sobre a documentação do SDK do Adobe Mobile, consulte [SDK do iOS 4.x para Soluções da Experience Cloud.](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html?lang=pt-BR)

   >[!IMPORTANT]
   >
   >A partir do iOS 9, a Apple introduziu um recurso chamado App Transport Security (ATS). Esse recurso tem como objetivo melhorar a segurança da rede, garantindo que seus aplicativos usem somente protocolos e cifras padrão do setor. Esse recurso é ativado por padrão, mas você tem opções de configuração que fornecem opções para trabalhar com ATS. Para obter detalhes sobre ATS, consulte [App Transport Security.](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/app-transport-security.html?lang=pt-BR)

* **Forneça os seguintes recursos no player de mídia:**

   * _Uma API para assinar eventos do player_ - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * _Uma API que fornece informações sobre o player_ - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

## Implementação do SDK

>[!IMPORTANT]
>
>A partir da versão 2.3.0, o SDK é distribuído via XCFrameworks.
>
>A versão 2.3.0 do SDK exige o Xcode 12.0 ou mais recente e, se aplicável, o Cocoapods 1.10.0 ou mais recente.

* Sempre que um arquivo binário de biblioteca for mencionado, sua substituição XCFramework deverá ser usada em vez disso:
   * MediaSDK.a > MediaSDK.xcframework
   * MediaSDK_TV.a > MediaSDKTV.xcframework
* Se você adicionar manualmente o Adobe XCFrameworks ao seu projeto, verifique se ele não está incorporado.

1. Adicione a biblioteca [baixada](/help/getting-started/download-sdks.md) do SDK do Media ao projeto.

   1. Verifique se os componentes de software a seguir existem no diretório `libs`:

      * `ADBMediaHeartbeat.h`: o arquivo do cabeçalho Objective-C usado para APIs de rastreamento de heartbeat no iOS.
      * `ADBMediaHeartbeatConfig.h`: o arquivo do cabeçalho Objective-C usado na configuração do SDK.
      * `MediaSDK.a`: um binário multiarquitetura habilitado para código de bits que contém as compilações de biblioteca para dispositivos iOS (armv7, armv7s, arm64) e simuladores (i386 e x86_64).

         Esse binário deve ser vinculado quando o destino for um aplicativo iOS.

      * `MediaSDK_TV.a`: um binário multiarquitetura habilitado para código de bits, que apresente as compilações de biblioteca para novos dispositivos Apple TV (arm64) e simuladores (x86_64).

         Esse binário deve ser vinculado quando o destino for pretendido para um aplicativo da Apple TV (tvOS).
   1. Adicione a biblioteca ao projeto:

      1. Abra o Xcode IDE e o seu aplicativo.
      1. No **[!UICONTROL Navegador do projeto]**, arraste o diretório `libs` e solte-o no seu projeto.

      1. Certifique-se de que as caixas de seleção **[!UICONTROL Copiar itens se necessário]** e **[!UICONTROL Criar grupos]** estejam marcadas e que nenhuma das caixas de seleção em **[!UICONTROL Adicionar ao destino]** estejam selecionadas.

      ![Escolher opções](assets/choose-options_ios.png)

      1. Clique em **[!UICONTROL Concluir]**.
      1. No **[!UICONTROL Navegador do projeto]**, selecione o seu aplicativo e os seus destinos.
      1. Vincule as estruturas e bibliotecas necessárias na seção **[!UICONTROL Estruturas vinculadas]** e **[!UICONTROL Bibliotecas]** na guia **[!UICONTROL Geral]**.

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

Para obter informações sobre a migração de 1.x para 2.x, consulte a documentação Implementação herdada .)

## Configuração de um aplicativo nativo para tvOS

Com o lançamento da nova Apple TV, agora é possível criar aplicativos para execução no ambiente tvOS nativo. Você pode criar um aplicativo puramente nativo, usando qualquer uma das várias estruturas disponíveis no iOS, ou criar seu aplicativo usando modelos XML e JavaScript. A partir da versão 2.0 do SDK do Media, o suporte para tvOS está disponível. Para mais informações sobre tvOS, consulte o [Site do desenvolvedor do tvOS.](https://developer.apple.com/tvos/)

Execute as seguintes etapas no projeto Xcode. Este guia foi escrito supondo que seu projeto tem um público-alvo que é um aplicativo da Apple TV direcionado ao tvOS:

1. Arraste o arquivo de biblioteca `VideoHeartbeat_TV.a` para a pasta `lib` do seu projeto.

1. Na guia **[!UICONTROL Criar fases]** do destino do seu aplicativo tvOS, expanda a seção **[!UICONTROL Link binário com bibliotecas]** e adicione as seguintes bibliotecas:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
