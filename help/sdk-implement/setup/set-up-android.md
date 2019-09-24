---
seo-title: Configurar Android
title: Configurar Android
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Configurar Android{#set-up-android}

## Pré-requisitos

* **Obtain valid configuration parameters for the Media SDK
These parameters can be obtained from an Adobe representative after you set up your analytics account.**
* **Implement ADBMobile for Android in your application
For more information about the Adobe Mobile SDK documentation, see Android SDK 4.x for Experience Cloud Solutions.**[](https://marketing.adobe.com/resources/help/en_US/mobile/android/)
* **Forneça os seguintes recursos no reprodutor de mídia:**
   * *Uma API para assinar os eventos do reprodutor* - O SDK do Media exige a chamada de um conjunto de APIs simples quando ocorrerem eventos no reprodutor.
   * *Uma API que fornece informações sobre o reprodutor* - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

## Implementação do SDK

1. Adicione a biblioteca [baixada](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) do SDK do Media ao projeto.

   1. Expand the Android zip file (e.g., `MediaSDK-android-v2.*.zip`).
   1. Verify that the `MediaSDK.jar` file exists in the `libs/` directory.

   1. Adicione a biblioteca ao projeto.

      **IntelliJ IDEA:**

      1. Clique com o botão direito do mouse no painel **[!UICONTROL Navegação do projeto]**.
      1. Selecione **[!UICONTROL Abrir configurações do módulo]**.
      1. Em **[!UICONTROL Configurações do projeto]**, selecione **[!UICONTROL Bibliotecas]**.

      1. Click **[!UICONTROL +]** to add a new library.
      1. Selecione **[!UICONTROL Java]** e navegue até o arquivo `MediaSDK.jar`.

      1. Selecione os módulos nos quais planeja usar a biblioteca móvel.
      1. Clique em **[!UICONTROL Aplicar]** e em **[!UICONTROL OK]** para fechar a janela Configurações do módulo.
      **Eclipse:**

      1. No Eclipse IDE, clique com o botão direito do mouse no nome do projeto.
      1. Click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Add External Archives]** .
      1. Selecionar `MediaSDK.jar`.
      1. Clique em **[!UICONTROL Abrir]**.
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Configure Build Path]** .
      1. Clique nas guias **[!UICONTROL Ordem]** e **[!UICONTROL Exportar]**.

      1. Verifique se o arquivo `MediaSDK.jar` foi selecionado.


1. Importe a biblioteca.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Create the `MediaHeartbeatConfig` instance.

   Aqui está uma amostra de inicialização `MediaHeartbeatConfig`:

   ```java
   // Media Heartbeat Initialization 
   config.trackingServer = _<SAMPLE_HEARTBEAT_TRACKING_SERVER>_; 
   config.channel = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp =  <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName = <SAMPLE_PLAYER_NAME>; 
   config.ssl = <true/false>; 
   config.debugLogging = <true/false>; 
   ```

1. Implement the `MediaHeartbeatDelegate` interface.

   ```java
   public class VideoAnalyticsProvider implements Observer, MediaHeartbeatDelegate{}
   ```

   ```java
   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override 
   public MediaObject getQoSObject() { 
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>); 
   } 
   
   //Replace <currentPlaybackTime> with the video player current playback time 
   @Override 
   public Double getCurrentPlaybackTime() { 
       return <currentPlaybackTime>; 
   }
   ```

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` instance and the `MediaHertbeatDelegate` instance to create the `MediaHeartbeat` instance.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. Essa instância será usada para todos os eventos de rastreamento a seguir.

**Inclusão de permissões de aplicativo**

O aplicativo que usa o SDK do Media exige as seguintes permissões para enviar dados nas chamadas de rastreamento:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Para adicionar essas permissões, adicione as seguintes linhas no seu arquivo `AndroidManifest.xml` no diretório do projeto do aplicativo:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migração da versão 1.x para 2.x do Android**

Nas versões 2.x, todos os métodos públicos foram consolidados na classe `com.adobe.primetime.va.simple.MediaHeartbeat` para facilitar o trabalho dos desenvolvedores. Além disso, todas as configurações foram consolidadas na classe `com.adobe.primetime.va.simple.MediaHeartbeatConfig`

For detailed information about migrating from 1.x to 2.x, see [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
