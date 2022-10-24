---
title: Saiba mais sobre pré-requisitos para mídia de transmissão
description: Introdução à mídia de streaming do Adobe Analytics. Saiba o que é necessário para implementar o Adobe Analytics para mídia de streaming.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: e5d1d86a2534a8c0fac63948e37a14b1dc1e896e
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 98%

---

# Pré-requisitos{#prerequisites}

## Decisões {#decision}

Antes de começar a implementação de rastreamento, você tem algumas decisões antecipadas a serem tomadas em relação à implementação que faz mais sentido para a sua situação:

* **Media Analytics -** Uso dos SDKs do Media mais recentes (a implementação padrão recomendada) e/ou a API Media Collection (RESTful)
* **Marco -** A implementação de rastreamento mais antiga da Adobe.
* **APIs de inserção de dados -** Implementação do rastreamento sem usar os SDKs do Media

## Tarefas {#prereq-tasks}

Para uma implementação do *Media Analytics*, siga estas etapas antes de começar:

1. **Ativar a Experience Cloud.**

   É necessário implementar o Adobe Experience Platform Identity Service.

   O Serviço de identidade habilita a estrutura de identificação comum para os serviços principais, soluções, atributos do cliente e públicos-alvo da Experience Cloud, no serviço principal de pessoas. Funciona ao atribuir uma ID exclusiva e persistente para um visitante do site. Quando sua organização implementa o serviço de ID, essa ID permite identificar o mesmo visitante do site e seus dados em diferentes soluções da Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   O serviço de ID também pode substituir diferentes IDs específicas da solução (por exemplo, Analytics AID). Através da funcionalidade [IDs de clientes e Estados de autenticação](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=pt-BR), o serviço de ID permite que você passe suas próprias IDs de cliente para a Experience Cloud. No entanto, lembre-se de que o serviço de ID funciona somente com as soluções nas quais você já se inscreveu. Se você não estiver inscrito para acessar outros produtos, o serviço de ID não fornecerá o acesso.

   O serviço de ID é um componente integral de diversos recursos, aprimoramentos e serviços atuais e futuros da Experience Cloud. No momento, o serviço de ID é compatível com o [Analytics,](https://www.adobe.com/br/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/br/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/br/marketing-cloud/testing-targeting.html)

   Se você ainda não implementou o serviço de ID, agora é o momento de começar a pensar em uma estratégia de migração. Para obter mais informações sobre a importância e a função do serviço de identidade, consulte [Por que você deve prestar atenção no serviço de identidade.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Para obter informações adicionais sobre a Experience Cloud ID, consulte [Visão geral da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) e [Serviço de Identidade da Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR).

1. **Ativar relatórios do Adobe Analytics.**

   Para permitir relatórios no Analytics e ver os dados de conteúdo e anúncios coletados, consulte [Ativação de relatórios de mídia.](/help/media-reports/media-reports-enable.md)
