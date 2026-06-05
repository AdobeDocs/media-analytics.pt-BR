---
title: Saiba mais sobre os pré-requisitos para os serviços de streaming de mídia do Adobe
description: Introdução aos serviços de streaming de mídia. Saiba o que é necessário para a implementação do.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 10%

---

# Pré-requisitos {#prerequisites}

Antes de começar a implementar os serviços de streaming de mídia da Adobe, conclua as seguintes tarefas:

1. **Confirme seu modelo de preços**<br>
O modelo de preços atual do complemento Coleção de mídia de streaming do Customer Journey Analytics e do complemento Adobe Analytics para mídia de streaming é baseado em fluxos de vídeo. Se necessário, entre em contato com o representante de vendas ou com a equipe de conta da Adobe, pois o complemento é vendido separadamente para a Adobe Analytics e a Adobe Experience Platform.

1. **Habilitar Relatórios do Adobe Analytics** *(implementações somente do Analytics)*<br>
Para permitir relatórios no Analytics e visualizar os dados de conteúdo e anúncios coletados, é necessário habilitar os relatórios. Consulte [Configurar relatórios para implementações somente do Analytics](/help/reporting/setup/analytics-reporting.md).

1. **Configurar identidade**<br>

   Os requisitos de configuração de identidade diferem dependendo do método de implementação:

   * **Implementações do Edge**: a identidade é tratada por meio da configuração do namespace de identidade da Adobe Experience Platform. Nenhuma configuração separada do serviço de identidade é necessária. Consulte [visão geral da implementação do Edge](/help/implementation/edge/overview.md) para obter detalhes.

   * **Implementações somente do Analytics**: o Adobe Experience Platform Identity Service deve estar habilitado para identificar visitantes de forma consistente nas soluções da CX Enterprise. O Identity Service atribui uma ID exclusiva e contínua a cada visitante do site e permite que essa ID seja compartilhada em todas as soluções da CX Enterprise nas quais você está inscrito.

     Para obter mais informações, consulte a [documentação do Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR).

1. **Exibir os pré-requisitos adicionais para seu método de implementação**

   Dependendo de como você planeja implementar os serviços de mídia de transmissão, visualize os pré-requisitos de um dos seguintes métodos de implementação:

   * [Visão geral da implementação somente no Analytics](/help/implementation/analytics-only/overview.md)

   * [Visão geral da implementação do Edge](/help/implementation/edge/overview.md)

   Consulte a [Visão geral da implementação](/help/implementation/overview.md) para determinar qual método de implementação é adequado para você.
