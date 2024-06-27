---
title: Saiba mais sobre os pré-requisitos do complemento Adobe Streaming Media Collection
description: Introdução ao Complemento de coleção de mídia de streaming. Saiba o que é necessário para a implementação do.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 62%

---

# Pré-requisitos  {#prerequisites}

Antes de começar a implementar o Complemento Adobe Streaming Media Collection, conclua as seguintes tarefas:

1. **Revise a visão geral do complemento Coleção de mídia de transmissão**<br>
Antes de começar a implementar o Complemento de coleção de mídia de transmissão, reveja o [Visão geral do complemento Coleção de mídia de streaming](/help/media-overview.md) para garantir que atenda às suas necessidades.

1. **Confirme seu modelo de preços**<br>
O modelo de preços atual do complemento Adobe Streaming Media Collection baseia-se em transmissões de vídeo. Se necessário, entre em contato com o representante de vendas ou com a equipe de conta do Adobe, pois o complemento é vendido separadamente para Adobe Analytics e Adobe Experience Platform.

1. **Ativar o Adobe Analytics Reports**<br>
Para permitir relatórios no Analytics ou Customer Journey Analytics e exibir os dados de conteúdo e anúncios coletados, é necessário habilitar os relatórios. Consulte [Ativação de relatórios de mídia](/help/reporting/media-reports-enable.md).

1. **Implementar o Adobe Experience Platform Identity Service na Experience Cloud**

   O **Serviço de identidade** habilita a estrutura de identificação comum para os serviços principais, soluções, atributos do cliente e públicos da Experience Cloud no serviço principal de Pessoas. Funciona ao atribuir uma ID exclusiva e persistente para um visitante do site. Quando sua organização implementa o serviço de ID, essa ID permite identificar o mesmo visitante do site e seus dados em diferentes soluções da Experience Cloud.

   ![Gráfico do serviço de ID](assets/mc_id_service_graphic.png)

   O serviço de ID também pode substituir diferentes IDs específicas da solução (por exemplo, Analytics AID). Através da funcionalidade [IDs de clientes e Estados de autenticação](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=pt-BR), o serviço de ID permite que você passe suas próprias IDs de cliente para a Experience Cloud. No entanto, lembre-se de que o serviço de ID funciona somente com as soluções nas quais você já se inscreveu. Se você não estiver inscrito para acessar outros produtos, o serviço de ID não fornecerá o acesso.

   O serviço de ID é um componente integral de vários recursos, aprimoramentos e serviços da Experience Cloud. No momento, o serviço de ID é compatível com o [Analytics,](https://www.adobe.com/br/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/br/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/br/marketing-cloud/testing-targeting.html)

   Se você ainda não implementou o serviço de ID, agora é o momento de começar a pensar em uma estratégia de migração. Para obter mais informações sobre a importância e a função do serviço de identidade, consulte [Por que você deve prestar atenção no serviço de identidade.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Para obter informações adicionais sobre a Experience Cloud ID, consulte [Visão geral da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) e [Serviço de Identidade da Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR).

1. **Exibir os pré-requisitos adicionais para seu método de implementação**

   Dependendo de como você planeja implementar o Complemento de coleção de mídia de transmissão, exiba os pré-requisitos de um dos seguintes métodos de implementação:

   * [Pré-requisitos para implementações somente do Adobe Analytics](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Pré-requisitos para implementações do Edge](/help/implementation/edge/prerequisites-edge.md)

   Consulte a [Visão geral da implementação](/help/implementation/overview.md) para determinar qual método de implementação é adequado para você.
