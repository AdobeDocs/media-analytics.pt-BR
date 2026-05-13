---
title: Pré-requisitos para implementações somente do Adobe Analytics
description: Saiba mais sobre os pré-requisitos para usar o complemento Adobe Analytics para mídia de streaming para implementações exclusivas do Adobe Analytics
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
TQID: https://experienceleague.adobe.com/falbDtUtqAMtmtQs2jLpEvUKmwvATotVu8njuTNZ09k
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 243
ht-degree: 14%

---

# Pré-requisitos para implementações somente do Adobe Analytics

Os pré-requisitos descritos nesta seção são específicos para implementar o complemento Adobe Analytics para mídia de streaming em implementações exclusivas do Adobe Analytics (quando não estiver usando o Edge).

1. **Concluir os pré-requisitos gerais**<br>
Se você implementar os serviços de mídia de transmissão para implementações somente do Adobe Analytics ou para implementações do Edge, verifique se atende aos [pré-requisitos gerais](/help/getting-started/prereqs.md).

1. **Confirme se você tem uma implementação do Adobe Analytics**<br>
Ao implementar o complemento Adobe Analytics para mídia de streaming para uma implementação somente do Analytics, também é necessária uma implementação básica do Adobe Analytics. Consulte [Implementar o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) para obter mais informações.

1. **Obter a URL do servidor de rastreamento de mídia**<br>
Peça ao representante da Adobe Analytics o URL do servidor de rastreamento de mídia. Esta é a URL `collection-api-server` do Mobile SDK, do JavaScript SDK e do servidor de rastreamento da API não coletora do Roku. Os nomes de domínio para a implementação da API são: `[your_namespace].hb-api.omtrdc.net`.

1. **Baixe o Media SDK atual ou implemente as extensões necessárias**<br>
Dependendo do caminho de implementação, [baixe o SDK](/help/getting-started/download-sdks.md) atual para plataformas da Web, móveis ou OTT. As extensões necessárias devem ser implementadas para habilitar o complemento Adobe Analytics para mídia de streaming.

1. **Habilitar Relatórios do Adobe Analytics**<br>
Para permitir relatórios no Analytics e visualizar os dados de conteúdo e anúncios coletados, é necessário habilitar os relatórios no Analytics. Consulte [Ativação de relatórios de mídia](/help/reporting/media-reports-enable.md).
