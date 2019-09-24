---
seo-title: Teste 2 Interrupção de mídia
title: Teste 2 Interrupção de mídia
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# Teste 2: Interrupção da mídia{#test-media-interruption}

Esse caso de teste valida o comportamento de interrupção móvel. It is a required element of your certification request.

## Formulário de solicitação de certificação

**Baixe o formulário de solicitação de certificação aqui: ==&gt;Formulário de solicitação** de [certificação.](cert_req_form.docx)

## Procedimento de ensaio

Você deve concluir e registrar essas tarefas na seguinte ordem:

1. **Iniciar o media player**

   When the media player starts, the following calls are sent in the following order:

   1. Adobe Analytics (AppMeasurement) Start
   1. Media Analytics (heartbeats) Start
   1. Media Analytics (heartbeats) Adobe Analytics Start call requested
   The first two calls above contain additional metadata and variables. For call parameters and metadata, see Test call details.[](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   The third call above tells the Media Analytics server that the Media SDK requested that the Adobe Analytics Start call () be sent to the Adobe Analytics server.`pev2=ms_s`

1. **Reproduzir conteúdo principal por pelo menos 5 minutos sem interrupções**

   **Reprodução de conteúdo**

   During content playback, the Media SDK sends play calls (heartbeats) to the Media Analytics server every ten seconds.

   For call parameters and metadata, see Test call details.[](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Mover o aplicativo ou o navegador para o segundo plano**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **Trazer aplicativo ou navegador de volta ao primeiro plano**

   Ao voltar para o primeiro plano, a reprodução do conteúdo deve ser retomada.

1. **Reproduzir mídia de conteúdo principal por pelo menos 5 minutos sem interrupções**

   For call parameters and metadata, see Test Call Details.[](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Close media player**

   Nenhuma chamada de rastreamento adicional deve ser acionada depois que o player de mídia for fechado.

