---
title: Saiba mais sobre os pré-requisitos de streaming de mídia
description: Introdução à mídia de streaming do Adobe Analytics. Saiba o que é necessário para implementar o Adobe Analytics para mídia de streaming.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 50%

---

# Pré-requisitos {#prerequisites}

Complete as seguintes tarefas para implementar o Adobe Analytics para mídia de transmissão:

1. **Confirme seu modelo de preços de mídia vapor**<br>
O modelo de preços atual é baseado em fluxos de vídeo. Se necessário, entre em contato com seu representante de vendas ou gerente de conta para assinar uma nova Ordem de venda, pois o Streaming Media Analytics é vendido separadamente da Adobe Analytics.

1. **Confirme se você está implementando o Adobe Analytics**<br>
A mídia de streaming para Adobe Analytics também requer uma implementação básica da Adobe Analytics. Consulte [Implementar o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) para obter mais informações.

1. **Obter o URL do servidor de rastreamento de mídia**<br>
Peça ao representante da Adobe Analytics o URL do servidor de rastreamento de mídia. Este é o 
`collection-api-server` URL para o SDK móvel, o SDK do JavaScript e o servidor de rastreamento de api de não coleta para Roku. Os nomes de domínio para implementação da API são: `[your_namespace].hb-api.omtrdc.net`.

1. **Baixe o SDK do Media atual ou implemente as extensões necessárias**<br>
Dependendo do caminho de implementação, [baixar o SDK atual](download-sdks.md) para plataformas da Web, móveis ou over-the-top. As extensões necessárias devem ser implementadas para habilitar o Adobe Analytics para mídia de transmissão. Para obter informações sobre as extensões necessárias, consulte [Extensões Adobe](download-sdks.md#media-extension). (É NECESSÁRIO esclarecer se o SDK do Media ou obter a extensão)

1. **Ativar relatórios do Adobe Analytics**<br>
Para permitir relatórios no Analytics e exibir os dados de conteúdo e anúncios coletados, é necessário ativar os relatórios no Analytics. Consulte [Ativação de relatórios de mídia.](/help/reporting/media-reports-enable.md).

1. **Ativar a Experience Cloud**<br>


## Implementar o Serviço de identidade da Adobe Experience Platform. {#implement-id}

O **Serviço de identidade** permite a estrutura de identificação comum para os serviços, soluções e atributos e públicos-alvo do cliente do Experience Cloud no serviço principal Pessoas. Funciona ao atribuir uma ID exclusiva e persistente para um visitante do site. Quando sua organização implementa o serviço de ID, essa ID permite identificar o mesmo visitante do site e seus dados em diferentes soluções da Experience Cloud.

![Gráfico do serviço de ID](assets/mc_id_service_graphic.png)

O serviço de ID também pode substituir diferentes IDs específicas da solução (por exemplo, Analytics AID). Através da funcionalidade [IDs de clientes e Estados de autenticação](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=pt-BR), o serviço de ID permite que você passe suas próprias IDs de cliente para a Experience Cloud. No entanto, lembre-se de que o serviço de ID funciona somente com as soluções nas quais você já se inscreveu. Se você não estiver inscrito para acessar outros produtos, o serviço de ID não fornecerá o acesso.

O serviço de ID é um componente integral de vários recursos, aprimoramentos e serviços do Experience Cloud. No momento, o serviço de ID é compatível com o [Analytics,](https://www.adobe.com/br/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/br/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/br/marketing-cloud/testing-targeting.html)

Se você ainda não implementou o serviço de ID, agora é o momento de começar a pensar em uma estratégia de migração. Para obter mais informações sobre a importância e a função do serviço de identidade, consulte [Por que você deve prestar atenção no serviço de identidade.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

Para obter informações adicionais sobre a Experience Cloud ID, consulte [Visão geral da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) e [Serviço de Identidade da Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR).
