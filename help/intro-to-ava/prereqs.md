---
seo-title: Pré-requisitos
title: Pré-requisitos
uuid: 4 c 0 b 37 f 3-8615-4 cc 0-b 9 c 9-mov 029067064
translation-type: tm+mt
source-git-commit: 80208f1c4773857f7907be0b8566c55a03e6106c

---


# Pré-requisitos{#prerequisites}

## Decisions {#decision}

Antes de começar a implementação de rastreamento, você precisa tomar algumas decisões iniciais com relação ao tipo de implementação mais adequado à sua situação:

* **Media Analytics -** Uso dos SDKs de mídia mais recentes (a implementação padrão recomendada) e/ou a API de coleção de mídia (RESTful)
* **Marco -** A implementação de rastreamento mais antiga da Adobe
* **APIs de inserção de dados -** Implementação do rastreamento sem usar os SDKs de mídia

## Tarefas {#prereq-tasks}

For a *Media Analytics* implementation, here are the tasks you must complete before you begin:

1. **Ativar a Experience Cloud.**

   Você precisa implementar o Adobe Experience Platform Identity Service.

   O Serviço de identidade habilita a estrutura de identificação comum dos principais serviços, soluções e atributos do cliente da Experience Cloud e públicos-alvo no serviço principal Pessoas. Isso funciona ao atribuir uma ID exclusiva e persistente para um visitante do site. Quando a organização implementa o serviço de ID, isso permite que você identifique o mesmo visitante do site e os dados em soluções diferentes da Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   O serviço de ID também pode substituir as IDs específicas de diferentes soluções (por exemplo, Analytics AID). Através da funcionalidade de [IDs de cliente e da funcionalidade Estados de autenticação](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-authenticated-state.html), o serviço de ID permite que você passe suas próprias IDs de cliente para a Experience Cloud. Tenha em mente que o serviço de ID funciona apenas com as soluções que você já assinou. Se você não tiver assinado para acessar outros produtos, o serviço de ID não fornecerá o acesso.

   O serviço de ID é um componente integral de diversos recursos, aprimoramentos e serviços atuais e futuros da Experience Cloud. Currently, the ID service supports [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) and [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Para participar do Device Co-op da Adobe Experience Cloud, o serviço da Experience Cloud ID é necessário.

   Se você ainda não implementou o serviço de ID, agora é o momento de começar a pensar em uma estratégia de migração. For more information about the importance and role of the ID service, see [Why the Identity Service Should be on Your Radar.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >In the absence of any user ID information present on the media-specific calls, the default analytics [Fallback ID Methods](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) will apply.

   For additional information about the Experience Cloud ID, see [Experience Cloud ID Overview,](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) and [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/)

1. **Ativar relatórios do Adobe Analytics.**

   Para permitir relatórios no Analytics e ver os dados de conteúdo e anúncios coletados, consulte [Ativação de relatórios de mídia.](../media-reports/media-reports-enable.md)

