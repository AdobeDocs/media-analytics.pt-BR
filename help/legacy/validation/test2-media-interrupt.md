---
title: 'Teste 2: Interrupção de mídia'
description: Saiba mais sobre o teste de interrupção de mídia usado na validação.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/gVEDMjM05nDnzCB6l-9CjyUzoArcmyN4jgsjmjllRiY
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889beid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 100%

---

# Teste 2: Interrupção de mídia{#test-media-interruption}

Esse caso de teste valida o comportamento de interrupção em dispositivos móveis.

## Procedimento de teste

Você deve concluir e registrar essas tarefas na seguinte ordem:

1. **Iniciar o reprodutor de mídia**

   Quando o reprodutor de mídia é iniciado, as seguintes chamadas são enviadas na seguinte ordem:

   1. Início do Adobe Analytics (AppMeasurement)
   1. Início do Media Analytics (heartbeats)
   1. Chamada de início do Adobe Analytics do Media Analytics (Heartbeats) solicitada

   As primeiras duas chamadas acima contêm metadados e variáveis adicionais. Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   A terceira chamada acima informa ao servidor do Media Analytics que o SDK do Media solicitou que a chamada de Início do Adobe Analytics (`pev2=ms_s`) fosse enviada para o servidor do Adobe Analytics.

1. **Reproduzir o conteúdo principal por, pelo menos, 5 minutos sem interrupções**

   **Reprodução de conteúdo**

   Durante a reprodução do conteúdo, o SDK do Media envia chamadas de reprodução (heartbeats) para o servidor do Media Analytics a cada dez segundos.

   Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/legacy/validation/test-call-details.md#play-main-content)

   Veja também as instruções do [Rastreamento de anúncios](/help/use-cases/track-ads/track-ads-overview.md) da plataforma para obter informações adicionais sobre essas chamadas de anúncios.

1. **Mover o aplicativo ou o navegador para o segundo plano**

   Enquanto o aplicativo é executado em segundo plano, somente as chamadas `main:pause` devem ser enviadas para o servidor do Media Analytics, a partir da versão 1.6.6 e posterior do VHL.

1. **Trazer o aplicativo ou o navegador para o primeiro plano**

   Ao voltar para o primeiro plano, a reprodução do conteúdo deve ser retomada.

1. **Reproduzir o conteúdo principal por, pelo menos, 5 minutos sem interrupções**

   Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Fechar reprodutor de mídia**

   Nenhuma chamada de rastreamento adicional deve ser acionada após o fechamento do reprodutor de mídia.
