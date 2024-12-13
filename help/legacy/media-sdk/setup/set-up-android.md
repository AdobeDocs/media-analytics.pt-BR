---
title: Como configurar o SDK de mídia no Android
description: Siga estas etapas para configurar o aplicativo do SDK de mídia no Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 97%

---

# Configurar Android{#set-up-android}

Saiba como configurar a coleção de mídia de streaming para dispositivos Android.

>[!IMPORTANT]
>
>Com o fim do suporte para SDKs móveis da versão 4 em 31 de agosto de 2021, a Adobe também encerrará o suporte para o SDK do Media Analytics para iOS e Android.  Para obter mais informações, consulte [Perguntas frequentes sobre o fim do suporte do SDK do Media Analytics](/help/additional-resources/end-of-support-faqs.md).


## Pré-requisitos

* **Obter parâmetros de configuração válidos para o SDK do Media** Esses parâmetros podem ser obtidos de um representante da Adobe após a configuração da sua conta do Analytics.
* **Implementar o ADBMobile para Android em seu aplicativo** 
Para obter mais informações sobre a documentação do SDK do Adobe Mobile, consulte [SDK 4.x do Android para Soluções da Experience Cloud.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html?lang=pt-BR)

* **Forneça os seguintes recursos no player de mídia:**
   * *Uma API para assinar eventos do player* - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * *Uma API que fornece informações sobre o player* - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

## Implementação do SDK

1. Adicione a biblioteca baixada do SDK de mídia no projeto.

   1. Expanda o arquivo zip do Android (por exemplo, `MediaSDK-android-v2.*.zip`).
   1. Verifique se o arquivo `MediaSDK.jar` existe no diretório `libs/`.

   1. Adicione a biblioteca ao projeto.

      **IntelliJ IDEA:**

      1. Clique com o botão direito do mouse no painel **[!UICONTROL Navegação do projeto]**.
      1. Selecione **[!UICONTROL Abrir configurações do módulo]**.
      1. Em **[!UICONTROL Configurações do projeto]**, selecione **[!UICONTROL Bibliotecas]**.

      1. Clique em **[!UICONTROL +]** para adicionar uma nova biblioteca.
      1. Selecione **[!UICONTROL Java]** e navegue até o arquivo `MediaSDK.jar`.

      1. Selecione os módulos nos quais planeja usar a biblioteca móvel.
      1. Clique em **[!UICONTROL Aplicar]** e em **[!UICONTROL OK]** para fechar a janela Configurações do módulo.

      **Eclipse:**

      1. No Eclipse IDE, clique com o botão direito do mouse no nome do projeto.
      1. Clique em **[!UICONTROL Criar caminho]** > **[!UICONTROL Adicionar arquivos externos]** .
      1. Selecionar `MediaSDK.jar`.
      1. Clique em **[!UICONTROL Abrir]**.
      1. Clique com o botão direito novamente no projeto e clique em **[!UICONTROL Criar caminho]** > **[!UICONTROL Configurar construção de caminho]** .
      1. Clique nas guias **[!UICONTROL Ordem]** e **[!UICONTROL Exportar]**.

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

Para obter informações sobre a migração da versão 1.x para a 2.x, consulte a documentação de Implementação herdada.
