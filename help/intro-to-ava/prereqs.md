---
title: Pré-requisitos
description: null
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: ht
source-git-commit: 72cdf2d03ebae6998514c9092ab462c29345c9f9
workflow-type: ht
source-wordcount: '424'
ht-degree: 100%

---


# Pré-requisitos {#prerequisites}

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

   O serviço de ID também pode substituir diferentes IDs específicas da solução (por exemplo, Analytics AID). Através da funcionalidade [IDs de clientes e Estados de autenticação](https://docs.adobe.com/content/help/pt-BR/id-service/using/reference/authenticated-state.html), o serviço de ID permite que você passe suas próprias IDs de cliente para a Experience Cloud. No entanto, lembre-se de que o serviço de ID funciona somente com as soluções nas quais você já se inscreveu. Se você não estiver inscrito para acessar outros produtos, o serviço de ID não fornecerá o acesso.

   O serviço de ID é um componente integral de diversos recursos, aprimoramentos e serviços atuais e futuros da Experience Cloud. No momento, o serviço de ID é compatível com o [Analytics,](https://www.adobe.com/br/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/br/marketing-cloud/data-management-platform.html) e [Target.](https://www.adobe.com/br/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Para participar da Adobe Experience Cloud Device Co-op, é necessário o serviço de Experience Cloud ID.

   Se você ainda não implementou o serviço de ID, agora é o momento de começar a pensar em uma estratégia de migração. Para obter mais informações sobre a importância e a função do serviço de identidade, consulte [Por que você deve prestar atenção no serviço de identidade.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >Na ausência de qualquer informação de ID de usuário nas chamadas específicas de mídia, os [Métodos de ID de fallback](https://docs.adobe.com/content/help/pt-BR/analytics/technotes/visitor-identification.translate.html) de análise padrão serão aplicados.

   Para obter informações adicionais sobre a Experience Cloud ID, consulte [Visão geral da Experience Cloud ID](https://docs.adobe.com/content/help/pt-BR/id-service/using/intro/overview.html) e [Serviço de Identidade da Adobe Experience Platform.](https://docs.adobe.com/content/help/pt-BR/id-service/using/home.html)

1. **Ativar relatórios do Adobe Analytics.**

   Para permitir relatórios no Analytics e ver os dados de conteúdo e anúncios coletados, consulte [Ativação de relatórios de mídia.](/help/media-reports/media-reports-enable.md)

