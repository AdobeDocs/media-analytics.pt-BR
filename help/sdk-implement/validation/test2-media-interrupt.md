---
seo-title: Interrupção de mídia Test 2
title: Interrupção de mídia Test 2
uuid: eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# Teste 2: Interrupção de mídia{#test-media-interruption}

Esse caso de teste valida o comportamento de interrupção móvel. É um elemento obrigatório da solicitação de certificação.

## Formulário de solicitação de certificação

**Baixe o formulário de solicitação de certificação aqui: = = &gt;**  [Formulário de solicitação de certificação.](cert_req_form.docx)

## Procedimento de teste

Você deve concluir e registrar essas tarefas na seguinte ordem:

1. **Iniciar o player de mídia**

   Quando o player de mídia é iniciado, as chamadas a seguir são enviadas na seguinte ordem:

   1. Início do Adobe Analytics (appmeasurement)
   1. Início do Media Analytics (heartbeats)
   1. Chamada de início do Media Analytics (heartbeats) Adobe Analytics solicitada
   As primeiras duas chamadas acima contêm metadados e variáveis adicionais. Para obter parâmetros de chamada e metadados, consulte [Detalhes de chamada de teste.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   A terceira chamada acima diz ao servidor Media Analytics que o Media SDK solicitou que a chamada de início do Adobe Analytics (`pev2=ms_s`) seja enviada para o servidor do Adobe Analytics.

1. **Reproduzir conteúdo principal por pelo menos 5 minutos sem interrupções**

   **Reprodução de conteúdo**

   Durante a reprodução do conteúdo, o SDK de mídia envia chamadas de play (heartbeats) ao servidor do Media Analytics a cada dez segundos.

   Para obter parâmetros de chamada e metadados, consulte [Detalhes de chamada de teste.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Mover o aplicativo ou o navegador para o segundo plano**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **Trazer o aplicativo ou o navegador de volta para primeiro plano**

   Ao voltar para o primeiro plano, a reprodução do conteúdo deve ser retomada.

1. **Reproduzir mídia de conteúdo principal por pelo menos 5 minutos sem interrupções**

   Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Fechar o player de mídia**

   Nenhuma chamada de rastreamento adicional deve ser acionada depois que o player de mídia for fechado.

