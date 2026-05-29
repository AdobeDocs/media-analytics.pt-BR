---
title: Saiba mais sobre os pré-requisitos para os serviços de streaming de mídia do Adobe
description: Introdução aos serviços de streaming de mídia. Saiba o que é necessário para a implementação do.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: 489
ht-degree: 46%

---

# Pré-requisitos {#prerequisites}

Antes de começar a implementar os serviços de streaming de mídia da Adobe, conclua as seguintes tarefas:

1. **Revise a visão geral dos serviços de streaming de mídia da Adobe**<br>
Antes de começar a implementar os serviços de streaming de mídia, reveja a [visão geral dos serviços de streaming de mídia da Adobe](/help/media-overview.md) para ter certeza de que eles atendem às suas necessidades.

1. **Confirme seu modelo de preços**<br>
O modelo de preços atual do complemento Coleção de mídia de streaming do Customer Journey Analytics e do complemento Adobe Analytics para mídia de streaming é baseado em fluxos de vídeo. Se necessário, entre em contato com o representante de vendas ou com a equipe de conta da Adobe, pois o complemento é vendido separadamente para a Adobe Analytics e a Adobe Experience Platform.

1. **Habilitar Relatórios do Adobe Analytics**<br>
Para permitir relatórios no Analytics ou Customer Journey Analytics e visualizar os dados de conteúdo e anúncios coletados, é necessário habilitar os relatórios. Consulte [Ativação de relatórios de mídia](/help/implementation/media-sdk/setup/media-reports-enable.md).

1. **Implementar o Adobe Experience Platform Identity Service no CX Enterprise**

   O **Identity Service** habilita a estrutura de identificação comum para os principais serviços, soluções, atributos do cliente e públicos-alvo da CX Enterprise no serviço principal People. Funciona ao atribuir uma ID exclusiva e persistente para um visitante do site. Quando sua organização implementa o serviço de ID, essa ID permite identificar o mesmo visitante do site e seus dados em diferentes soluções da CX Enterprise.

   ![Gráfico do serviço de ID](assets/mc_id_service_graphic.png)

   O serviço de ID também pode substituir diferentes IDs específicas da solução (por exemplo, Analytics AID). Através da funcionalidade [IDs de clientes e Estados de autenticação](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=pt-BR), o serviço de ID permite que você passe suas próprias IDs de cliente para o CX Enterprise. No entanto, lembre-se de que o serviço de ID funciona somente com as soluções nas quais você já se inscreveu. Se você não estiver inscrito para acessar outros produtos, o serviço de ID não fornecerá o acesso.

   O serviço de ID é um componente integral de vários recursos, aprimoramentos e serviços do CX Enterprise. No momento, o serviço de ID é compatível com o [Analytics,](https://www.adobe.com/br/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/br/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/br/marketing-cloud/testing-targeting.html)

   Se você ainda não implementou o serviço de ID, agora é o momento de começar a pensar em uma estratégia de migração. Para obter mais informações sobre a importância e a função do serviço de identidade, consulte [Por que você deve prestar atenção no serviço de identidade.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Para obter informações adicionais sobre a Experience Cloud ID, consulte [Visão geral da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) e [Serviço de Identidade da Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR).

1. **Exibir os pré-requisitos adicionais para seu método de implementação**

   Dependendo de como você planeja implementar os serviços de mídia de transmissão, visualize os pré-requisitos de um dos seguintes métodos de implementação:

   * [Pré-requisitos para implementações somente do Adobe Analytics](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Pré-requisitos para implementações do Edge](/help/implementation/edge/prerequisites-edge.md)

   Consulte a [Visão geral da implementação](/help/implementation/overview.md) para determinar qual método de implementação é adequado para você.
