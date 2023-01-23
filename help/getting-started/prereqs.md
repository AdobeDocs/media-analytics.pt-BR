---
title: Saiba mais sobre os pré-requisitos de streaming de mídia
description: Introdução à mídia de streaming do Adobe Analytics. Saiba o que é necessário para implementar o Adobe Analytics para mídia de streaming.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: b022bed6b7be0cc97caaaf6b7bbc42474a57b400
workflow-type: ht
source-wordcount: '486'
ht-degree: 100%

---

# Pré-requisitos {#prerequisites}

Para implementar o Adobe Analytics para mídia de streaming, conclua as seguintes tarefas:

1. **Confirme seu modelo de preços de mídia de streaming**<br>
O modelo de preços atual é baseado em transmissões de vídeo. Se necessário, entre em contato com seu representante de vendas ou gerente de conta para assinar uma nova ordem de venda, pois o Analytics para mídia de streaming é vendido separadamente do Adobe Analytics.

1. **Confirme se você está implementando o Adobe Analytics**<br>
O streaming de mídia no Adobe Analytics também requer uma implementação básica do Adobe Analytics. Consulte [Implementar o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) para obter mais informações.

1. **Obter o URL do servidor de rastreamento de mídia**<br>
Solicite o URL do servidor de rastreamento de mídia ao seu representante do Adobe Analytics. Este é o 
`collection-api-server` URL do SDK móvel, do SDK do JavaScript e do servidor de rastreamento da API não coletora do Roku. Os nomes de domínio para a implementação da API são: `[your_namespace].hb-api.omtrdc.net`.

1. **Baixe o SDK de mídia atual ou implemente as extensões necessárias**<br>
Dependendo do caminho de implementação, [baixar o SDK atual](download-sdks.md) para plataformas da Web, móveis ou OTT. As extensões necessárias devem ser implementadas para ativar os caminhos de extensões do Adobe Analytics para mídia de streaming.

1. **Ativar relatórios do Adobe Analytics**<br>
Para permitir o uso de relatórios no Analytics e visualizar os dados de conteúdo e anúncios coletados, é necessário ativar os relatórios no Analytics. Consulte [Ativação de relatórios de mídia](/help/reporting/media-reports-enable.md).

1. **Ativar a Experience Cloud**<br>


## Implementar o Serviço de identidade da Adobe Experience Platform {#implement-id}

O **Serviço de identidade** habilita a estrutura de identificação comum para os serviços principais, soluções, atributos do cliente e públicos da Experience Cloud no serviço principal de Pessoas. Funciona ao atribuir uma ID exclusiva e persistente para um visitante do site. Quando sua organização implementa o serviço de ID, essa ID permite identificar o mesmo visitante do site e seus dados em diferentes soluções da Experience Cloud.

![Gráfico do serviço de ID](assets/mc_id_service_graphic.png)

O serviço de ID também pode substituir diferentes IDs específicas da solução (por exemplo, Analytics AID). Através da funcionalidade [IDs de clientes e Estados de autenticação](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=pt-BR), o serviço de ID permite que você passe suas próprias IDs de cliente para a Experience Cloud. No entanto, lembre-se de que o serviço de ID funciona somente com as soluções nas quais você já se inscreveu. Se você não estiver inscrito para acessar outros produtos, o serviço de ID não fornecerá o acesso.

O serviço de ID é um componente integral de vários recursos, aprimoramentos e serviços da Experience Cloud. No momento, o serviço de ID é compatível com o [Analytics,](https://www.adobe.com/br/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/br/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/br/marketing-cloud/testing-targeting.html)

Se você ainda não implementou o serviço de ID, agora é o momento de começar a pensar em uma estratégia de migração. Para obter mais informações sobre a importância e a função do serviço de identidade, consulte [Por que você deve prestar atenção no serviço de identidade.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

Para obter informações adicionais sobre a Experience Cloud ID, consulte [Visão geral da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) e [Serviço de Identidade da Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR).
