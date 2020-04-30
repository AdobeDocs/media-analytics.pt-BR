---
title: Configurar Android
description: Configuração do aplicativo SDK do Media para implementação no Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Configurar Android {#set-up-android}

## Pré-requisitos

* **Obter parâmetros de configuração válidos para o SDK do Media** Esses parâmetros podem ser obtidos de um representante da Adobe após a configuração da sua conta do Analytics.
* **Implementar o ADBMobile para Android em seu aplicativo** 
Para obter mais informações sobre a documentação do SDK do Adobe Mobile, consulte [SDK 4.x do Android para Soluções da Experience Cloud.](https://docs.adobe.com/content/help/pt-BR/mobile-services/android/overview.html)
* **Forneça os seguintes recursos no player de mídia:**
   * *Uma API para assinar eventos do player* - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * *Uma API que fornece informações sobre o player* - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

## Implementação do SDK

1. Adicione a biblioteca [baixada](/help/sdk-implement/download-sdks.md#download-2x-sdks) do SDK do Media ao projeto.

   1. Expanda o arquivo zip do Android (por exemplo, `MediaSDK-android-v2.*.zip`).
   1. Verifique se o arquivo `MediaSDK.jar` existe no diretório `libs/`.

   1. Adicione a biblioteca ao projeto.

      **IntelliJ IDEA:**

      1. Right click your project in the **[!UICONTROL Project navigation]** panel.
      1. Selecionar **[!UICONTROL Open Module Settings]**.
      1. Em **[!UICONTROL Project Settings]**, selecione **[!UICONTROL Libraries]**.

      1. Click **[!UICONTROL +]** to add a new library.
      1. Selecione **[!UICONTROL Java]** e navegue até o arquivo `MediaSDK.jar`.

      1. Selecione os módulos nos quais planeja usar a biblioteca móvel.
      1. Click **[!UICONTROL Apply]** and then **[!UICONTROL OK]** to close the Module Settings window.
      **Eclipse:**

      1. No Eclipse IDE, clique com o botão direito do mouse no nome do projeto.
      1. Clique em  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. Selecionar `MediaSDK.jar`.
      1. Clique em **[!UICONTROL Open]**.
      1. Clique novamente no projeto com o botão direito do mouse e clique em **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]** .
      1. Clique nas guias **[!UICONTROL Order]** e **[!UICONTROL Export]** .

      1. Verifique se o arquivo `MediaSDK.jar` foi selecionado.


1. Importe a biblioteca.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Crie a instância `MediaHeartbeatConfig`.

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

1. Implemente a interface `MediaHeartbeatDelegate`.

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

1. Crie a instância `MediaHeartbeat`.

   Use a instância `MediaHeartbeatConfig` e `MediaHertbeatDelegate` para criar a instância `MediaHeartbeat`.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Certifique-se de que a instância `MediaHeartbeat` possa ser acessada e *não seja desalocada até o final da sessão*. Essa instância será usada para todos os eventos de rastreamento a seguir.

**Adicionar permissões de aplicativo**

O aplicativo que usa o SDK de mídia requer as seguintes permissões para enviar dados em chamadas de rastreamento:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Para adicionar essas permissões, adicione as seguintes linhas no seu arquivo `AndroidManifest.xml` no diretório do projeto do aplicativo:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migração da versão 1.x para 2.x do Android**

Nas versões 2.x, todos os métodos públicos foram consolidados na classe `com.adobe.primetime.va.simple.MediaHeartbeat` para facilitar o trabalho dos desenvolvedores. Além disso, todas as configurações foram consolidadas na classe `com.adobe.primetime.va.simple.MediaHeartbeatConfig`

Para obter informações detalhadas sobre a migração de 1.x para 2.x, consulte [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
