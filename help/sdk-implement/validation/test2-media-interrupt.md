---
title: Teste 2 Interrupção de mídia
description: Este tópico descreve o teste de interrupção de mídia usado na validação.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Teste 2: Interrupção da mídia{#test-media-interruption}

Esse caso de teste valida o comportamento de interrupção móvel. É um elemento obrigatório da sua solicitação de certificação.

## Formulário de solicitação de certificação

**Baixe o formulário de solicitação de certificação aqui: ==&gt;Formulário de solicitação** de [certificação.](cert_req_form.docx)

## Procedimento de ensaio

Você deve concluir e registrar essas tarefas na seguinte ordem:

1. **Iniciar o media player**

   Quando o player de mídia é iniciado, as seguintes chamadas são enviadas na seguinte ordem:

   1. Início do Adobe Analytics (AppMeasurement)
   1. Início do Media Analytics (pulsações)
   1. Chamada de início do Adobe Analytics de mídia (pulsações) solicitada pelo Adobe Analytics
   As primeiras duas chamadas acima contêm metadados e variáveis adicionais. Para obter parâmetros de chamada e metadados, consulte Detalhes da chamada [de teste.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   A terceira chamada acima informa ao servidor do Media Analytics que o SDK de mídia solicitou que a chamada (`pev2=ms_s`) de Início do Adobe Analytics fosse enviada para o servidor do Adobe Analytics.

1. **Reproduzir conteúdo principal por pelo menos 5 minutos sem interrupções**

   **Reprodução de conteúdo**

   Durante a reprodução do conteúdo, o SDK de mídia envia chamadas de reprodução (pulsações) para o servidor do Media Analytics a cada dez segundos.

   Para obter parâmetros de chamada e metadados, consulte Detalhes da chamada [de teste.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Mover o aplicativo ou o navegador para o segundo plano**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **Trazer aplicativo ou navegador de volta ao primeiro plano**

   Ao voltar para o primeiro plano, a reprodução do conteúdo deve ser retomada.

1. **Reproduzir mídia de conteúdo principal por pelo menos 5 minutos sem interrupções**

   Para obter parâmetros de chamada e metadados, consulte Detalhes da chamada [de teste.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Fechar media player**

   Nenhuma chamada de rastreamento adicional deve ser acionada depois que o player de mídia for fechado.

