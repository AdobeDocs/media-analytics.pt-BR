---
title: Teste 2 Interrupção de mídia
description: Saiba mais sobre o teste de interrupção de mídia usado na validação.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 96%

---

# Teste 2: Interrupção da mídia {#test-media-interruption}

Esse caso de teste valida o comportamento de interrupção móvel.

## Procedimento de teste

Você deve concluir e registrar essas tarefas na seguinte ordem:

1. **Iniciar o reprodutor de mídia**

   Quando o reprodutor de mídia é iniciado, as seguintes chamadas são enviadas na seguinte ordem:

   1. Início do Adobe Analytics (AppMeasurement)
   1. Início do Media Analytics (heartbeats)
   1. Chamada de início do Adobe Analytics do Media Analytics (Heartbeats) solicitada

   As primeiras duas chamadas acima contêm metadados e variáveis adicionais. Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   A terceira chamada acima informa ao servidor do Media Analytics que o SDK do Media solicitou que a chamada de Início do Adobe Analytics (`pev2=ms_s`) fosse enviada para o servidor do Adobe Analytics.

1. **Reproduzir o conteúdo principal por, pelo menos, 5 minutos sem interrupções**

   **Reprodução de conteúdo**

   Durante a reprodução do conteúdo, o SDK do Media envia chamadas de reprodução (heartbeats) para o servidor do Media Analytics a cada dez segundos.

   Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Veja também as instruções da plataforma de [Rastrear anúncios](/help/sdk-implement/track-ads/track-ads-overview.md) para obter informações adicionais sobre essas chamadas de anúncios.

1. **Mover o aplicativo ou o navegador para o segundo plano**

   Enquanto o aplicativo é executado em segundo plano, somente as chamadas `main:pause` devem ser enviadas para o servidor do Media Analytics, a partir da versão 1.6.6 e posterior do VHL.

1. **Trazer o aplicativo ou o navegador para o primeiro plano**

   Ao voltar para o primeiro plano, a reprodução do conteúdo deve ser retomada.

1. **Reproduzir o conteúdo principal por, pelo menos, 5 minutos sem interrupções**

   Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Fechar reprodutor de mídia**

   Nenhuma chamada de rastreamento adicional deve ser acionada após o fechamento do reprodutor de mídia.
