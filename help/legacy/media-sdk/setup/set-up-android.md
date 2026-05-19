---
title: Como configurar o SDK de mídia no Android
description: Siga estas etapas para configurar o aplicativo do SDK de mídia no Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/re7nZLD9IwvufJGicWLArSwdIi6h518q3ZMDf6oqaCI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 459
ht-degree: 86%

---

# Configurar Android{#set-up-android}

Saiba como configurar serviços de mídia de transmissão para dispositivos Android.

>[!IMPORTANT]
>
>Com o fim do suporte para SDKs móveis da versão 4 em 31 de agosto de 2021, a Adobe também encerrará o suporte para o SDK do Media Analytics para iOS e Android.  Para obter mais informações, consulte [Perguntas frequentes sobre o fim do suporte do SDK do Media Analytics](/help/additional-resources/end-of-support-faqs.md).


## Pré-requisitos

* **Obter parâmetros de configuração válidos para o Media SDK**
Esses parâmetros podem ser obtidos de um representante da Adobe após a configuração da sua conta do Analytics.
* **Implementar o ADBMobile para Android em seu aplicativo**
Para obter mais informações sobre a documentação do Adobe Mobile SDK, consulte [Android SDK 4.x para Soluções da Experience Cloud.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html?lang=pt-BR)

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
